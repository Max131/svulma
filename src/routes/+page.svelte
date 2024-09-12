<script>
  import { Tabs, Tab } from "$lib/Tabs";
  import { Modal } from "$lib/Modal";
  import { Field, Input } from "$lib/Form";
  import { Candy, Skull, User } from "lucide-svelte";
  import { Button, Buttons } from "$lib/Button";
  import Icon from "$lib/Icon";

  let modal1 = false;
</script>

<svelte:head>
  <link href="https://unpkg.com/boxicons@2.1.4/css/boxicons.min.css" rel="stylesheet" />
</svelte:head>

<section class="section">
  <h1 class="title">Svulma</h1>
  <p class="subtitle">
    A simple <a href="https://bulma.io" target="_blank" rel="noopener noreferrer">Bulma</a>
    components for <a href="https://svelte.dev" target="_blank" rel="noopener noreferrer">Svelte</a>
  </p>
</section>

<section class="section">
  <h2 class="title is-3">Buttons</h2>
  <Buttons>
    <Button appearance="is-primary">
      <Icon icon={User}></Icon>
      <span>Lorem</span>
    </Button>
    <Button appearance="is-success">
      <span>Ipsum</span>
      <Icon icon={Candy}></Icon>
    </Button>
    <Button appearance="is-info">Dolor</Button>
    <Button appearance="is-warning">Sit</Button>
    <Button appearance="is-danger">Amet</Button>
  </Buttons>
  <Buttons>
    <Button appearance="is-link">Lorem</Button>
    <Button appearance="is-light">Ipsum</Button>
    <Button appearance="is-white">Dolor</Button>
    <Button appearance="is-dark">Sit</Button>
    <Button appearance="is-text">Amet</Button>
  </Buttons>
  <Buttons>
    <Button appearance="is-ghost">Lorem</Button>
    <Button appearance="is-success" isLoading>Ipsum</Button>
    <Button appearance="is-info" isLight>Dolor</Button>
    <Button appearance="is-warning" isOutlined>Sit</Button>
    <Button appearance="is-danger" isRounded>Amet</Button>
  </Buttons>
  <Buttons size="are-small">
    <Button appearance="is-primary" isOutlined isLight isRounded isLoading>Lorem</Button>
    <Button appearance="is-success">Ipsum</Button>
    <Button appearance="is-info" size="is-large">Dolor</Button>
    <Button appearance="is-warning">Sit</Button>
    <Button appearance="is-danger">Amet</Button>
  </Buttons>
</section>

<section class="section">
  <h2 class="title is-3">Icons</h2>
  <h3 class="title is-5">Icon string (boxicons)</h3>
  <Icon icon="bx bxs-heart-circle bx-lg" size="is-large" />
  <h3 class="title is-5">Icon Component (lucide icons)</h3>
  <Icon icon={{ icon: Candy, size: 42 }} size="is-large" />
</section>

<section class="section">
  <h2 class="title is-3">Tabs</h2>
  <div class="my-4">
    <Tabs>
      <Tab label="User" icon="bx bxs-pear">
        <p>
          Lorem consectetur aut ex id eveniet Expedita perferendis molestias corrupti quas tempora.
          Maiores sapiente similique voluptas incidunt ducimus ducimus. Sint minima cumque nulla ea
          porro. Expedita dolore debitis delectus dolorum.
        </p>
      </Tab>
      <Tab label="Config" icon={Skull}>
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
      <Tab label="Paragraph">
        <div class="content">
          <p>
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Eveniet harum, tenetur eum,
            labore ratione repellat mollitia commodi veniam soluta voluptatum tempore eius quas
            nobis officia deleniti consequatur voluptatibus laudantium ea.
          </p>
          <p>
            Accusantium dolorem eos iure inventore odio expedita officia quasi error impedit veniam!
            Aliquam inventore expedita nihil, quidem odio soluta in sequi debitis impedit corporis,
            facere sunt possimus culpa quo consequatur!
          </p>
        </div>
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

<section class="section">
  <h3 class="title is-3">Forms</h3>
  <Field>
    <Input />
  </Field>
  <Field>
    <Input icon="bx bx-envelope" />
  </Field>
  <Field>
    <Input iconRight={User} />
  </Field>
  <Field hasAddons>
    <Input value="lorem ipsum" />
    <div class="control">
      <button class="button is-warning">Button</button>
    </div>
  </Field>
  <Field hasAddons>
    <div class="control">
      <butto class="button is-static">With reveal button</butto>
    </div>
    <Input typeInput="password" value="myownpassword" revealButton />
  </Field>
</section>
