<svelte:head>
	<title>Docker</title>
</svelte:head>

<!-- Titel pagina -->
<section>
	<section>
		<h3>Hey Bastards!</h3>
		<img src="https://media.giphy.com/media/XO8RMtRaK73isIt0i2/giphy.gif" style="height: 200px" />
	</section>
	<section>
		<h3>Heads-up!</h3>
		<img src="https://media.giphy.com/media/z1QdOcqwRdMDxocKrR/giphy.gif" style="height: 200px" />
		<p>We zijn live op YouTube!</p>
	</section>
	<section
		data-notes="Introductie, korte uitleg wat we deze kennissessie gaan bespreken. Niet de inhoud, dat is volgende slide"
	>
		<div
			style="display: flex; flex-direction: row; align-items: center; justify-content: center; margin: 0 auto 4rem auto; gap: 4rem;"
		>
			<img
				src="/images/swb-logo.svg"
				alt="Software Bastards logo"
				style="height: 180px; aspect-ratio: 1/1; background: transparent;"
			/>
			<span>X</span>
			<img
				src="/images/docker/logo.svg"
				alt="Docker logo"
				style="height: 180px; aspect-ratio: 1/1; background: transparent;"
			/>
		</div>
		<h3>Docker<small style="vertical-align: baseline;">, of:</small></h3>
	</section>
	<section data-background="https://media.giphy.com/media/befaYZCgtZfZm/giphy.gif">
		<h3>It works on <span style="text-decoration: underline;">our</span> machine!</h3>
	</section>
</section>

<!-- Inhoud -->
<section>
	<section>
		<h2>Disclaimer!</h2>
		<img src="https://media.giphy.com/media/kyLhFEKgNoWin9Ezu4/giphy.gif" style="height: 300px" />
		<p>Dit is de basis.</p>
	</section>
	<section>
		<h2>Inhoud</h2>
		<ul>
			<li><a href="#/2">Wat is Docker nou eigenlijk?</a></li>
			<li><a href="#/3">Tijd voor termen!</a></li>
			<li><a href="#/4">Hoe ziet dit er uit?</a></li>
			<li><a href="#/5">Throwing it all together: Docker Compose!</a></li>
			<li><a href="#/6">Iets moeilijker: Netwerken</a></li>
			<li><a href="#/7">Hoe/wat bij Software Bastards</a></li>
		</ul>
	</section>
</section>

<!-- Docker basics uitleg -->
<section>
	<section>
		<h2>Wat is Docker nou eigenlijk?</h2>
		<img src="/images/docker/explain.webp" style="height: 300px" />
	</section>
	<section>
		<h2>Meer dan de memes</h2>
		<div style="display: flex; flex-direction: row; gap: 16px; justify-content: center;">
			<img src="/images/docker/it_works_on_my_machine.webp" style="height: 400px;" />
		</div>
	</section>
	<section>
		<h2>Virtual Machines</h2>
		<img src="/images/docker/xzibit_vm.jpeg" style="height: 400px;" />
	</section>
	<section>
		<h2>Docker</h2>
		<img src="/images/docker/xzibit_docker.jpeg" style="height: 400px;" />
	</section>
</section>
<section>
	<section>
		<h2>Tijd voor termen!</h2>
		<img src="https://media.giphy.com/media/TXRHoV5Dvv7cA/giphy.gif" style="height: 300px;" />
	</section>
	<section>
		<h2>Images</h2>
		<ul>
			<li>Blueprint van je applicatie</li>
			<li>Geversioneerd</li>
			<li>Uitbreidbaar (tot een punt)</li>
			<li>Basis voor Containers</li>
		</ul>
	</section>
	<section>
		<h2>Containers</h2>
		<ul>
			<li>Instantie van je applicatie</li>
			<li>Op basis van een image</li>
			<li>Draait op host OS</li>
		</ul>
	</section>
	<section>
		<h2>Configuraties</h2>
		<ul>
			<li>
				Kan bepaald worden door applicatie
				<ul>
					<li>Environment variabelen</li>
					<li>Configuratie bestanden</li>
				</ul>
			</li>
			<li>
				Kan bepaald worden door image
				<ul>
					<li>Ports</li>
					<li>Volumes</li>
				</ul>
			</li>
			<li>Mee te geven via docker command</li>
		</ul>
	</section>
	<section data-auto-animate>
		<h2>Palate cleanser</h2>
		<img
			src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExM2VueDdmeHZ3dGp2a254MzI4aGI0Z3h2eGdiam9vdnBtYXo3OHJ0dCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/3oKIPnAiaMCws8nOsE/giphy.gif"
			style="height: 300px;"
		/>
	</section>
</section>

<!-- DockerFile uitleg -->
<section>
	<section data-auto-animate>
		<h2 data-id="code-title">Hoe ziet dit er uit?</h2>
		<pre data-id="code-animation">
					<code class="hljs docker" data-trim data-line-numbers="1-6|1|3|5|6">
						FROM nginx:alpine

						EXPOSE 80

						COPY default.conf /etc/nginx/conf.d/
						COPY dist /usr/share/nginx/html/
					</code>
				</pre>
	</section>
	<section>
		<h2>Bouw je image</h2>
		<pre data-id="code-animation">
					<code class="hljs console" data-trim>
						docker build -t custom-nginx-server .
					</code>
				</pre>
	</section>
	<section>
		<h2>Start de container</h2>
		<pre data-id="code-animation">
					<code class="hljs console" data-trim>
						docker run\
							-p 8080:80\
							--name custom-nginx-app\
							custom-nginx-server
					</code>
				</pre>
	</section>
	<section>
		<h2>Of met veel configuratie</h2>
		<pre data-id="code-animation">
					<code class="hljs console" data-trim>
						docker run\
							-p 8080:80\
							-v ./dist:/usr/share/nginx/html:ro\
							-v ./nginx.conf:/etc/nginx/nginx.conf:ro\
							-e NGINX_ENTRYPOINT_QUIET_LOGS=1\
							--name nginx-app\
							nginx:alpine
					</code>
				</pre>
	</section>
</section>

<!-- Docker Compose uitleg -->
<section>
	<section data-auto-animate>
		<h2>Throwing it all together: Docker Compose!</h2>
		<img src="https://media.giphy.com/media/KEYEpIngcmXlHetDqz/giphy.gif" style="height: 300px;" />
	</section>
	<section>
		<h2>Custom NGINX image</h2>
		<pre data-id="code-animation">
				<code class="hljs yaml" data-trim data-line-numbers="1-7|6-7|5|4|1-7">
					version: "3.7"
					services:
						custom-nginx-app:
							image: custom-nginx-server
							container_name: custom-nginx-app
							ports:
								- 8080:80
				</code>
			</pre>
	</section>
	<section>
		<h2>Docker Compose aanslingeren</h2>
		<pre data-id="code-animation">
					<code class="hljs console" data-trim>
						docker compose up
					</code>
				</pre>
	</section>
	<section>
		<h2>Base NGINX image</h2>
		<pre data-id="code-animation">
				<code class="hljs yaml" data-trim data-line-numbers="1-12|6-7|8-10|11-12|5|4|1-12">
					version: "3.7"
					services:
						nginx-app:
							image: nginx:alpine
							container_name: nginx-app
							ports:
								- 8080:80
							volumes:
								- ./dist:/usr/share/nginx/html:ro
								- ./nginx.conf:/etc/nginx/nginx.conf:ro
							environment:
								NGINX_ENTRYPOINT_QUIET_LOGS: 1
				</code>
			</pre>
	</section>
</section>

<!-- Ietwat advanced Docker dingen -->
<section>
	<section>
		<h2>Iets moeilijker: Netwerken</h2>
		<img src="https://media.giphy.com/media/Zx1KzuQBR8wIbrm81t/giphy.gif" style="height: 200px" />
	</section>
	<section>
		<h2>Netwerken</h2>
		<ul>
			<li>Gedeelde netwerken</li>
			<li>Meerdere netwerken per container</li>
			<li>Eenvoudige referentie op zelfde netwerk</li>
		</ul>
	</section>
	<section>
		<h2>Netwerk voorbeeld</h2>
		<pre data-id="code-animation">
					<code class="hljs yaml" data-trim data-line-numbers="20-21|3-11|8-9|12-18|17-18|10-11">
						version: "3.7"
						services:
							nginx-app:
								image: custom-nginx-server
								container_name: nginx-app
								ports:
									- 8080:80
								networks:
									- custom-network
								environment:
									SOME_SECOND_APP_REFERENCE: 'http://second-app'
							second-app:
								image: custom-second-server
								container_name: second-app
								ports:
									- 8081:80
								networks:
									- custom-network
						
						networks:
							custom-network:
					</code>
				</pre>
	</section>
</section>

<section>
	<section>
		<h2>Hoe/wat bij Software Bastards</h2>
		<ul>
			<li>
				Websites
				<ul>
					<li>Software Bastards</li>
					<li>Bodyindustrie</li>
					<li>Haarwensen</li>
				</ul>
			</li>
			<li>Keycloak</li>
			<li>Portaal (Uren)</li>
		</ul>
	</section>
	<section>
		<h2>NodeJS voorbeeld</h2>
		<pre data-id="code-animation">
					<code class="hljs docker" data-trim data-line-numbers="1-11|1|3|5|7|9-11">
						FROM node:lts-alpine

						WORKDIR /app

						COPY ./dist/apps/web/site .

						EXPOSE 3000

						RUN npm ci --production

						CMD ["node", "/app/index.js"]
					</code>
				</pre>
	</section>
</section>

<section>
	<section>
		<h2>Recap!</h2>
		<img src="https://media.giphy.com/media/n6MeACfIHgGiiGIokv/giphy.gif" style="height: 300px;" />
	</section>
	<section>
		<h2>We hebben besproken</h2>
		<ul>
			<li>Hoe/wat Docker</li>
			<li>Hoe/wat Images</li>
			<li>Hoe/wat Containers</li>
			<li>Wat voorbeelden</li>
			<li>Docker Compose</li>
			<li>Hoe/wat bij Software Bastards</li>
		</ul>
	</section>
	<section>
		<h2>Gefeliciteerd! *</h2>
		<img src="/images/docker/devops_engineer.jpeg" style="height: 300px" />
		<p><small>*= Grapje, er komt nog veel meer bij kijken</small></p>
	</section>
</section>

<section data-background="https://media.giphy.com/media/3o7btZ1Gm7ZL25pLMs/giphy.gif">
	<h2>Vragen?</h2>
</section>
