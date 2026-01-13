<template>
	<section id="contact" class="text-center py-5 px-3 px-md-5 bg-contact">
		<h3 class="fw-bold mb-4">Contact</h3>
		<div class="container">
			<div class="row align-items-start">
				<div class="col-lg-6 mb-4 mb-lg-0">
					<form action="">
						<div class="mb-3" id="name">
							<label for="name" class="form-label">Name</label>
							<input
							type="text"
							class="form-control bg-white"
							id="name"
							placeholder="First Name, M.I, Last Name"
							/>
						</div>
						<div class="mb-3" id="email">
							<label for="email" class="form-label">Email address</label>
							<input
							type="email"
							class="form-control bg-white"
							id="email"
							placeholder="Email"
							/>
						</div>
						<div class="mb-3" id="message">
							<label for="message" class="form-label">Message</label>
							<textarea class="form-control bg-white" id="message" rows="6" placeholder="Message"></textarea>
						</div>
						<button type="button" class="mb-3 rounded-pill" id="button">Submit</button>
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
</section>
</template>

