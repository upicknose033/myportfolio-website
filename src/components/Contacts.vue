<template>
	<section id="contact" class="text-center py-5 px-3 px-md-5 bg-contact">
		<h3 class="fw-bold mb-4">Contact</h3>
		<div class="container">
			<div class="row align-items-start">
				<div class="col-lg-6 mb-4 mb-lg-0">
					<form @submit.prevent="submitForm">
						<div class="mb-3" id="name">
							<label for="name" class="form-label">Name</label>
							<input
							v-model="name"
							type="text"
							class="form-control bg-white"
							id="name"
							placeholder="First Name, M.I, Last Name"
							/>
						</div>
						<div class="mb-3" id="email">
							<label for="email" class="form-label">Email address</label>
							<input
							v-model="email"
							type="email"
							class="form-control bg-white"
							id="email"
							placeholder="Email"
							/>
						</div>
						<div class="mb-3" id="message">
							<label for="message" class="form-label">Message</label>
							<textarea v-model="message" class="form-control bg-white" id="message" rows="6" placeholder="Message"></textarea>
						</div>
						<button type="submit" class="mb-3 rounded-pill" id="button" :disabled="isLoading">
							{{
								isLoading ? "Sending . . .": "Submit"
								}}
						</button>
					</form>
				</div>
				<div class="col-lg-6">
					<div class="map-container">
						<iframe 
						src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3861.7532577739894!2d120.98344151072989!3d14.556097785866276!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3397cb658633c953%3A0xa241ae88ec52197a!2sStar%20City!5e0!3m2!1sen!2sph!4v1759325620818!5m2!1sen!2sph" 
						class="map-iframe" 
						allowfullscreen="" 
						loading="lazy" 
						referrerpolicy="no-referrer-when-downgrade"
						title="Star City Location Map">
					</iframe>
				</div>
			</div>
		</div>
	</div>
	<div class="d-flex flex-wrap justify-content-center gap-3 mt-4">
		<a href="https://about.gitlab.com/" target="_blank" aria-label="Visit my Gitlab profile">
			<img class="contact-sites" src="/images/gitlab.png" alt="Gitlab">
		</a>
		<a href="https://github.com/" target="_blank" aria-label="Visit my Github profile">
			<img class="contact-sites" src="/images/github.png" alt="Github">
		</a>
		<a href="https://www.linkedin.com/in/pedro-jose-siapuatco-b5a9611ba/" target="_blank" aria-label="Visit my LinkedIn profile">
			<img class="contact-sites" src="/images/linkedin.png" alt="LinkedIn">
		</a>
	</div>
<div class = "d-flex justify-content-end mt-2">
	<div ref ="recaptchaContainer"></div>
</div>
</section>
</template>

<script setup>
	import { ref, onMounted } from "vue";
	import { Notyf } from "notyf";
	import "notyf/notyf.min.css"

	const WEB3FORMS_ACCESS_KEY = "e8a40f9f-6952-42c4-aa30-61b804165668";
	const name = ref("")
	const email = ref("")
	const message = ref("")

// Loading state
	const isLoading = ref(false);

	const notyf = new Notyf();

// configurations needed for the recaptcha
	const SITE_KEY = '6LcWlEksAAAAAAWJDsbczdlsYNamjZinVVX85Ma8';
	const recaptchaContainer = ref(null);
	const recaptchaWidgetId = ref(null);
	const recaptchaToken = ref('');


// Callback called by reCAPTCHA when successful
function onRecaptchaSuccess(token) {
  recaptchaToken.value = token;
}

// Callback when expired
function onRecaptchaExpired() {
  recaptchaToken.value = '';
}

// Function to render the reCAPTCHA widget
function renderRecaptcha() {
  if (!window.grecaptcha) {
    console.error('reCAPTCHA not loaded');
    return;
  }

  recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
    sitekey: SITE_KEY,
    size: 'normal', // or 'compact'
    callback: onRecaptchaSuccess,
    'expired-callback': onRecaptchaExpired,
  });
}

// Function to reset reCAPTCHA 
function resetRecaptcha() {
  if (recaptchaWidgetId.value !== null) {
    window.grecaptcha.reset(recaptchaWidgetId.value);
    recaptchaToken.value = '';
  }
}



onMounted(() => {
  // This code waits for the Google reCAPTCHA library to load, then renders the reCAPTCHA widget using onMounted hook. 
  // The widget is rendered with grecaptcha.render(), which requires a sitekey. 
  // Callback functions handle success and expiration events. 
  // reCAPTCHA is reset upon form submission to clear the token.
  const interval = setInterval(() => {
    if (window.grecaptcha && window.grecaptcha.render) {
      renderRecaptcha();
      clearInterval(interval);
    }
  }, 100);

  onBeforeUnmount(() => {
    clearInterval(interval);
  });
});
// The submitForm() handler function sends the form data to web3forms and displays success or failure notifications toast
	const submitForm = async () => {
		if(!recaptchaToken.value){
			notyf.error('Please verify that you are not a robot');
			return;
		}



	isLoading.value = true;
		try {
			const response = await fetch("https://api.web3forms.com/submit", {
				method: "POST",
				headers: {
					"Content-Type": "application/json",
					Accept: "application/json",
				},
				body: JSON.stringify({
					access_key: WEB3FORMS_ACCESS_KEY,
					name: name.value,
					email: email.value,
					message: message.value,
				}),
			});
			const result = await response.json();
			if (result.success) {
				console.log(result);
				isLoading.value = false;

				notyf.success("Message Sent!");
			}
		}
		catch(error){
			console.log(error);

			isLoading.value = false;
			notyf.error("Failed to send message.")


		}
	}
</script>
