<svelte:head>
	<title>Kubernetes</title>
</svelte:head>

<!-- Titel pagina -->
<section>
	<section>
		<h3>Hey Bastards!</h3>
		<img
			src="https://media.giphy.com/media/XO8RMtRaK73isIt0i2/giphy.gif"
			alt="Hello!"
			style="height: 200px"
		/>
		<aside class="notes">
			Korte introductie praatje, even de aandacht trekken en iedereen stil krijgen
		</aside>
	</section>
	<section>
		<h3>Heads-up!</h3>
		<img
			src="https://media.giphy.com/media/z1QdOcqwRdMDxocKrR/giphy.gif"
			alt="We are live!"
			style="height: 200px"
		/>
		<p>We zijn live op YouTube!</p>
		<aside class="notes">
			Uitleggen dat we live zijn, even vragen of mensen hun devices willen muten enzo voor minimale
			afleiding.
		</aside>
	</section>
	<section>
		<h2>Hoi, ik ben Dymion</h2>
		<img src="/images/k8s/dymion.png" alt="Hello!" style="height: 300px" />
		<aside class="notes">
			Beginnen met de presentatie, eerst een hele kleine grappige introductie op basis van het
			nummer Escape (The Pina Colada Song)
		</aside>
	</section>
	<section>
		<h2>Ik hou van...</h2>
		<ul>
			<li>Piña coladas</li>
			<li>Long walks on the beach</li>
			<li>Muziek</li>
		</ul>
		<aside class="notes">
			De eerste twee list-items zijn uit het nummer, de 3e is het aanhaakpunt voor deze presentatie!
			Uitleggen dat deze presentatie ook ongeveer over muziek zal gaan, maar dan anders...
		</aside>
	</section>
	<section>
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
				src="/images/k8s/logo.svg"
				alt="Kubernetes logo"
				style="height: 180px; aspect-ratio: 1/1; background: transparent;"
			/>
		</div>
		<h3>Kubernetes<small style="vertical-align: baseline;">, of:</small></h3>
		<aside class="notes">
			We gaan het namelijk hebben over Kubernetes! En aangezien Kubernetes een orchestrator is...
		</aside>
	</section>
	<section data-background="https://media.giphy.com/media/3ohhwBL1q1I66srvAA/giphy.gif">
		<h3>Ik ga liever naar een ander soort orkest...</h3>
		<aside class="notes">
			Is het net alsof we naar een soort orkest gaan (maar ik wil toch liever naar een ander soort
			orkest)
		</aside>
	</section>
</section>

<!-- Inhoud -->
<section>
	<section>
		<h2>Op reis!</h2>
		<img
			src="https://media.giphy.com/media/m6dm34kEpM1gc/giphy.gif"
			alt="Parrot riding a bike"
			style="height: 300px"
		/>
		<p>Mijn ervaring met Kubernetes</p>
		<aside class="notes">
			We gaan op reis! Door mijn (Dymion's) ervaringen met Kubernetes als Frontend ontwikkelaar!
		</aside>
	</section>
	<section>
		<h2>Inhoud</h2>
		<ul>
			<li><a href="#/2">Één orkest, vele genres</a></li>
			<li><a href="#/3">Basis principes</a></li>
			<li><a href="#/4">De configuratie files</a></li>
			<li><a href="#/5">Taking control: Kubectl!</a></li>
			<li><a href="#/6">Gerelateerde concepten!</a></li>
			<li><a href="#/7">Hoe/wat bij Software Bastards?</a></li>
			<li><a href="#/8">Hoe/wat voor mij?</a></li>
		</ul>
		<aside class="notes">De inhoud spreekt aardig voor zich hoop ik</aside>
	</section>
</section>

<!-- Uitleg van verschillende soorten rollen -->
<section>
	<section>
		<h2>Één orkest, vele genres</h2>
		<ul>
			<li>KCNA<br /><small>Kubernetes and Cloud Native Associate</small></li>
			<li>KCSA<br /><small>Kubernetes and Cloud Native Security Associate</small></li>
			<li>CKAD<br /><small>Certified Kubernetes Application Developer</small></li>
			<li>CKA<br /><small>Certified Kubernetes Administrator</small></li>
			<li>CKS<br /><small>Certified Kubernetes Security Specialist</small></li>
		</ul>
		<aside class="notes">
			Een overzicht van de verschillende Kubernetes rollen, afkortingen + de volledig uitgeschreven
			rol naam
		</aside>
	</section>
	<section>
		<h2>CKAD</h2>
		<ul>
			<li>Bouwen van de apps</li>
			<li>Deployen van de apps</li>
			<li>Beheren/monitoren van de apps</li>
		</ul>
		<aside class="notes">
			Mijn ervaring is voornamelijk in de rol van CKAD ontwikkelaar. Ik bouw de apps, deploy ze, en
			kan ze beheren/monitoren
		</aside>
	</section>
</section>

<section>
	<section>
		<h2>Basis principes</h2>
		<img
			src="https://media.giphy.com/media/hk0Etc9B2U06tISuDY/giphy.gif"
			alt="Shall we discuss terms?"
			style="height: 300px;"
		/>
		<aside class="notes">
			Voordat we er echt diep in duiken, laten we eens gaan kijken naar wat basis termen die wel
			handig zijn!
		</aside>
	</section>
	<section>
		<h2>Pods</h2>
		<ul>
			<li>Enkele container (one-container-per-pod)</li>
			<li>Verzameling van containers</li>
			<li>Eigenlijk nooit direct zelf aangemaakt</li>
		</ul>
		<aside class="notes">
			Om te beginnen: Pods! Pods zijn instanties van je containers, een of meerdere tegelijkertijd.
			Je maakt ze eigenlijk nooit zelf aan, maar met behulp van zogenoemde Deployments (hierover
			straks meer).
		</aside>
	</section>
	<section>
		<h2>Nodes</h2>
		<ul>
			<li>Hier draaien de pods</li>
			<li>"Poten" van je cluster</li>
		</ul>
		<aside class="notes">
			De Pods draaien op je nodes, en de nodes zijn als het ware je (fysieke of virtuele) servers.
			Het idee van de nodes in een Kubernetes cluster is dat je er meerdere hebt, en wanneer er een
			uit valt/gaat je dus kan terugvallen op andere nodes binnen het cluster.
		</aside>
	</section>
	<section>
		<h2>Controlplane</h2>
		<ul>
			<li>Managed de nodes en pods</li>
			<li>
				Meerdere "components"
				<ul>
					<li>API</li>
					<li>Scheduler</li>
					<li>Verschillende controllers</li>
				</ul>
			</li>
		</ul>
		<aside class="notes">
			Als laatste term hebben we de zogenoemde Controlplane. De Controlplane is als het ware het
			brein van je Kubernetes cluster en die zorgt er voor dat al je pods en nodes lief blijven
			samenwerken. De Controlplane bestaat uit meerdere onderdelen, zoals de API, scheduler en
			verschillende controllers, maar ze werken allemaal samen om je cluster in leven te houden. Je
			kan wegkomen met een enkele Controlplane, maar aangeraden wordt om ook deze over meerdere
			servers te laten draaien.
		</aside>
	</section>
</section>

<!-- YAML uitleg -->
<section>
	<section>
		<h2>De configuratie files</h2>
		<aside class="notes">
			Cool, termen zijn besproken, laten we nu wat dieper de voorbeelden in gaan door naar de
			configuratie bestanden te kijken!
		</aside>
	</section>
	<!-- Uitleg van de "kinds" -->
	<section>
		<h2>Kinds</h2>
		<ul>
			<li>Geeft aan wat het doel is van dit stukje YAML</li>
			<li>Officiele en community-supported</li>
			<li>Spec is afhankelijk van de kind</li>
		</ul>
		<aside class="notes">
			Om te beginnen hebben we de kind, dit geeft aan wat het doel is van je YAML configuratie. Denk
			bijvoorbeeld aan het definieren van een Deployment, Service of Ingress, dit zijn allemaal
			verschillende soorten Kinds. Er zijn officiele en community supported opties, zoals
			bijvoorbeeld de Zalando Postgres operator die een 'postgresql' kind toevoegt. De kind bepaalt
			ook hoe je de verdere specificaties moet invullen, dus welke opties er te configureren zijn.
		</aside>
	</section>
	<!-- Uitleg deployments & Services -->
	<section>
		<h2>Deployments & Services</h2>
		<ul>
			<li>Deployment is voor je pod</li>
			<li>Service is voor toegang</li>
		</ul>
		<aside class="notes">
			De 2 kinds waar ik zelf het meest mee te maken heb gehad zijn de Deployments en de Services.
			Een Deployment maakt een pod aan waarin je containers draaien. Een Service gebruik je om
			specifieke poorten te exponsen van een applicatie die netwerking nodig heeft.
		</aside>
	</section>
	<!-- Simpele NGINX deployment + Service voorbeeld -->
	<section>
		<h2>NGINX voorbeeldje</h2>
		<pre data-id="code-animation">
			<code
				class="hljs yaml"
				data-trim
				data-line-numbers="1-35|1-2|3-6|7-11|12|13-15|16-22|24-25|26-27|28-35">
				apiVersion: apps/v1
				kind: Deployment
				metadata:
					name: nginx-deployment
					labels:
						app.kubernetes.io/name: proxy
				spec:
					replicas: 3
					selector:
						matchLabels:
							app: nginx
					template:
						metadata:
							labels:
								app: nginx
						spec:
							containers:
							- name: nginx
								image: nginx:stable
								ports:
								- containerPort: 80
									name: http-web-svc
				---
				apiVersion: v1
				kind: Service
				metadata:
					name: nginx-service
				spec:
					selector:
						app.kubernetes.io/name: proxy
					ports:
					- name: name-of-service-port
						protocol: TCP
						port: 80
						targetPort: http-web-svc
			</code>
		</pre>
		<aside class="notes">
			Laten we eens kijken naar een Deployment + Service voorbeeld met NGINX! Om te beginnen
			definieren we de Deployment, deze bestaat uit wat metadata die we later kunnen gebruiken om
			naar deze deployment te kunnen refereren. Vervolgens definieren we de specificaties voor de
			deployment, we willen dat er 3 replicas van de pod draaien. Hierna gaan we de template
			definieren, wederom wat metadata voor identificatie en wederom een specificatie voor deze
			template. In dit geval gaat het dus om een NGINX container op basis van de nginx:stable image
			waarbij we poort 80 exposen via de naam 'http-web-svc'. Hierna definieren we de service
			(uiteraard weer met wat metadata) waarmee we de NGINX poort gaan exposen naar de buitenwereld.
			Omdat we in de Deployment de service een naampje hebben gegeven, kunnen we die nu gebruiken
			als referentie!
		</aside>
	</section>
	<!-- Ingress uitleg -->
	<section>
		<h2>Netwerktoegang voor Ingress</h2>
		<pre data-id="code-animation">
			<code class="hljs yaml" data-trim data-line-numbers="1-21|1-2|3-4|5-6|7-10|11-13|14-17|18-21">
				apiVersion: networking.k8s.io/v1
				kind: Ingress
				metadata:
					name: nginx
				spec:
					ingressClassName: nginx
					tls:
					- hosts:
						- example.example.com
							secretName: quickstart-example-tls
					rules:
					- host: example.example.com
						http:
							paths:
							- path: /
								pathType: Prefix
								backend:
									service:
										name: nginx
										port:
											number: 80
			</code>
		</pre>
		<aside class="notes">
			Ingresses zijn bedoeld om, met behulp van HTTP/HTTPS, je applicaties naar buiten je cluster
			toegankelijk te maken. Dit kan met behulp van SSL certificaten en domeinen, maar laten we voor
			het gemak er even doorheen lopen! Om te beginnen starten we weer met de kind definitie,
			gevolgd door de benodigde metadata. Hierna beginnen we met de het definieren van de
			configuratie, starten met de ingressClassName, deze bepaald namelijk welke Ingress Controller
			er gebruik moet worden (in ons geval NGINX). Hierna kunnen we aangeven welk certificaat (in
			dit geval TLS) gebruikt moet worden en in welke secret het certificaat moet worden opgeslagen.
			Vervolgens gaan we het domein configureren, in dit voorbeeld "example.example.com", waarna we
			kunnen aangeven op welk pad binnen dit domein de applicatie toegankelijk moet zijn. Als
			allerlaatste koppelen we deze ingress aan onze NGINX service waarbij we aangeven om welke
			poort het gaat.
		</aside>
	</section>
	<!-- Statefulset & Persistent Volume Claim uitleg -->
	<section>
		<h2>Statefulsets & Persistent Volume Claims</h2>
		<ul>
			<li>Soms hebben je applicaties state</li>
			<!-- Vaak nodig voor non-cloud-native apps -->
			<li>Statefulset combineert pods</li>
			<li>PVCs is een data claim op je cluster</li>
		</ul>
		<aside class="notes">
			Meeste applicaties die op kubernetes draaien zijn zogenoemde stateless of cloud-native
			applicaties. Maar soms komt het voor dat je een non-cloud-native app op je cluster moet
			draaien. In deze gevallen wordt er aangeraden om gebruik te maken van een Statefulset, waarin
			je meerdere pods die bij elkaar moeten blijven draaien kan combineren. Ook is het mogelijk om
			(gedeelde) persistente data te gebruiken in je applicaties, zoals bijvoorbeeld een mount voor
			geuploadde files of misschien configuratie-bestanden. In deze gevallen kan je een zogenoemde
			Persistent Volume Claim (PVC) toepassen, waarmee je een blok aan data claimed op je cluster.
			Ik zelf heb niet heel veel ervaring met deze 2 oplossingen, maar wel hebben we bij een klant
			gebruik gemaakt van een PVC voor een SQLite database voor een Lighthouse Server instantie.
		</aside>
	</section>
</section>

<!-- KubeCTL uitleg -->
<section>
	<section data-auto-animate>
		<h2>KubeCTL</h2>
		<img src="https://media.giphy.com/media/L4UbIh0Zqm1Kr0BRzA/giphy.gif" alt="Take control" />
		<aside class="notes">
			Nu we wat mooie configuraties hebben opgesteld, willen we deze natuurlijk ook kunnen toepassen
			op ons cluster, en dit is waar KubeCTL ons bij kan helpen!
		</aside>
	</section>
	<section>
		<h2>Toepassen van een configuratie</h2>
		<pre data-id="code-animation">
			<code class="hljs console" data-trim>
				kubectl apply -f deployment.yaml
			</code>
		</pre>
		<aside class="notes">
			Mijn ervaring met KubeCTL is vrij gelimiteerd, en het kwam voornamelijk neer op het toepassen
			van configuraties. Ik heb me er wel destijds dieper in verdiept en je zou bijvoorbeeld ook
			configmaps kunnen aanmaken en dergelijke, maar in mijn ervaring werden ook dat soort dingen
			altijd vastgelegd in een YAML configuratie. Het toepassen van een configuratie doe je met
			behulp van het commando op het scherm.
		</aside>
	</section>
	<section>
		<h2>Maar...</h2>
		<ul>
			<li>Je hebt geen waarheid</li>
			<li>Liever vastgelegd in git</li>
		</ul>
		<aside class="notes">
			Maar... Liever doe je niks met KubeCTL direct want je hebt geen waarheid. Mooi dat Pietje
			productie heeft gefixed, maar hoe zag die YAML file er uit, en waarom was het uberhaupt nodig
			nadat Klaas productie omver had getrokken met een kubectl commando? Je legt dit soort dingen
			liever vast in bijvoorbeeld git, met behulp van pipelines e.d., ipv dingen direct op het
			cluster te wijzigen.
		</aside>
	</section>
</section>

<!-- Gerelateerde concepten zoals GitOps en Helm-charts -->
<section>
	<section>
		<h2>Gerelateerde concepten</h2>
		<img
			src="https://media.giphy.com/media/xUj3Mfn12fNmDa8kmu/giphy.gif"
			alt="I relate to that"
			style="height: 200px"
		/>
		<aside class="notes">
			Dit brengt ons dan ook naar een klein uitstapje van gerelateerde concepten!
		</aside>
	</section>
	<section>
		<h2>Gerelateerde concepten</h2>
		<ul>
			<li>
				Kubernetes sausje
				<ul>
					<li>Openshift</li>
					<li>Rancher</li>
					<li>Cloud oplossingen (AKS, EKS, GKS)</li>
				</ul>
			</li>
			<li>GitOps concept (ArgoCD)</li>
			<li>
				Customization
				<ul>
					<li>Helm-charts</li>
					<li>Kustomize</li>
				</ul>
			</li>
		</ul>
		<aside class="notes">
			Om te beginnen zijn er verschillende sausjes voor Kubernetes, denk hierbij aan RedHats
			Openshift, aan SUSE's Rancher of aan verschillende cloud oplossingen zoals AKS, EKS en GKS. Al
			deze oplossingen zijn over het algemeen doorgebouwd op de Kubernetes basis en voegen zo extra
			functionaliteiten toe. Een ander conceptn dat steeds vaker naar voren komt wanneer er over
			Kubernetes wordt gesproken is GitOps, waarbij je Git repo de waarheid is en met behulp van
			bijvoorbeeld tools als ArgoCD je Kubernetes cluster aansturen en voorzien van de benodigde
			configuraties. Als laatste zijn er ook verschillende oplossingen voor het dynamisch
			configurabel maken van de configuraties, zoals bijvoorbeeld Helm-charts of de Kustomize tool.
		</aside>
	</section>
</section>

<!-- Uitleg van hoe/wat bij SB en onze klanten en waarom dit interessant is om in te verdiepen -->
<section>
	<section>
		<h2>Hoe/wat bij Software Bastards?</h2>
		<ul>
			<li>Onze klanten</li>
			<li>Micro-frontends</li>
			<li>Managed cluster</li>
		</ul>
		<aside class="notes">
			Binnen Software Bastards doen we ook al veel met Kubernetes, maar niet altijd direct zelf. We
			zien het veelal terug bij onze klanten, waarbij onze ontwikkelaars er misschien niet zelf
			direct mee te maken hebben maar wel indirect dus toepassen. Verder hanteren wij voor onze
			applicaties al een micro-frontend/micro-service architectuur, waarbij we goed nadenken over de
			rollen en de samenhang van de verschillende onderdelen zodat deze al zoveel mogelijk richting
			de cloud-native oplossing gaan. Daarnaast zijn we op het moment verschillende managed cluster
			oplossingen aan het bekijken om ook voor onze applicaties uiteindelijk richting een kubernetes
			oplossing te gaan.
		</aside>
	</section>
</section>

<!-- Expliciete mention van managed kubernetes clusters/getting started voor jezelf, maybe mention van cursussen voor CKAD -->
<section>
	<section>
		<h2>Hoe/wat voor mij?</h2>
		<ul>
			<li>CKAD cursus/certificering</li>
			<li>Minikube/k3s/Rancher Desktop</li>
			<li>Managed clusters</li>
			<li>Docker</li>
		</ul>
		<aside class="notes">
			Super tof allemaal, maar hoe kan je hier nou zelf mee beginnen? Ik was zelf begonnen met een
			cursus voor CKAD volgen zodat ik in elk geval een lading basis kennis had, hierna ben ik
			begonnen met kijken naar het lokaal draaiend krijgen van een Kubernetes cluster (en dan
			specifiek een zogenoemd single-node-cluster) d.m.v. tools als Minikube, k3s en Rancher
			Desktop. Dit werkte niet altijd geheel feilloos, dus op een gegeven moment ben ik gaan kijken
			naar managed clusters waarbij ik enkel de focus hoefde te leggen op het ontwikkelen van de
			verschillende applicaties die ik op mijn cluster wilde draaien. De allerlaatste tip die ik heb
			is echter veel eenvoudiger: Leer Docker, en dan met name hoe je applicatie cloud-native (dus
			technisch gezien stateless) bouwt.
		</aside>
	</section>
</section>

<section data-background="https://media.giphy.com/media/l0CLV6LkWccT6CwG4/giphy.gif">
	<h2>Vragen?</h2>
	<aside class="notes">Zijn er nog vragen?</aside>
</section>
