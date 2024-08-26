<script>
	import { Tabs, Tab } from "$lib/Tabs";
	import { Modal } from "$lib/Modal";

	let modal1 = false;
</script>

<section class="section">
	<h1 class="title">Svulma</h1>
	<p class="subtitle">
		A simple <a href="https://bulma.io" target="_blank" rel="noopener noreferrer">Bulma</a>
		components for <a href="https://svelte.dev" target="_blank" rel="noopener noreferrer">Svelte</a>
	</p>
</section>

<section class="section">
	<h2 class="title is-3">Tabs</h2>
	<div class="my-4">
		<Tabs>
			<Tab label="User">
				<p>
					Lorem consectetur aut ex id eveniet Expedita perferendis molestias corrupti quas tempora.
					Maiores sapiente similique voluptas incidunt ducimus ducimus. Sint minima cumque nulla ea
					porro. Expedita dolore debitis delectus dolorum.
				</p>
			</Tab>
			<Tab label="Config">
				<article class="media">
					<figure class="media-left">
						<p class="image is-64x64">
							<img src="https://bulma.io/assets/images/placeholders/128x128.png" alt="" />
						</p>
					</figure>
					<div class="media-content">
						<div class="content">
							<p>
								<strong>John Smith</strong> <small>@johnsmith</small> <small>31m</small>
								<br />
								Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin ornare magna eros, eu
								pellentesque tortor vestibulum ut. Maecenas non massa sem. Etiam finibus odio quis feugiat
								facilisis.
							</p>
						</div>
					</div>
				</article>
			</Tab>
		</Tabs>
	</div>
</section>

<section class="section">
	<h2 class="title is-3">Modals</h2>

	<button class="button is-info" on:click={() => (modal1 = true)}>Open Modal</button>
	<div data-theme="light">
		<Modal bind:active={modal1}>
			<div class="box">
				<p>
					Lorem ipsum dolor sit amet consectetur adipisicing elit. Modi maxime necessitatibus in
					tenetur fugit nisi accusamus veritatis, similique porro aperiam!
				</p>
			</div>
		</Modal>
	</div>
</section>
