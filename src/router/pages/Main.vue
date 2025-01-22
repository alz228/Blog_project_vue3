<template>
  <div>
    <h1 style="page__title">Demo project - blog on vue</h1>
    <p class="ul__main-title">
      <strong>Description of the Blog Web Application</strong>
    </p>
    <ul>
      <ul>
        <p class="ul__title"><strong>Viewing Posts:</strong></p>
        <ul>
          <li>
            Post data (title and description) is fetched via an API and
            displayed on the main page.
          </li>
          <li>
            The ability to navigate to a detailed post page to view the full
            content.
          </li>
        </ul>

        <p class="ul__title"><strong>Content Management:</strong></p>
        <ul>
          <li>Creating new posts through the built-in interface.</li>
          <li>Deleting posts upon user request.</li>
        </ul>

        <p class="ul__title"><strong>Additional Features:</strong></p>
        <ul>
          <li>Responsive design for seamless viewing on any device.</li>
          <li>Notifications about successful post creation or deletion.</li>
        </ul>
      </ul>
    </ul>

    <div class="navbar__btns">
      <my-button class="big-button" @click="$router.push('/blog')"
        >Go to blog</my-button
      >
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
h1 {
  color: teal;
}

.ul__main-title {
  margin-top: 30px;
  font-size: 20px;
}

.ul__title {
  margin-top: 30px;
}

ul {
  margin-top: 10px;
}
li {
  margin-left: 20px;
  margin-top: 5px;
}

li::marker {
  color: teal;
}

.big-button {
  width: 180px;
  height: 40px;
  font-size: 18px;

  align-items: center;
  justify-content: center;
  display: flex;

  margin-left: 20px;
  margin-top: 45px;
  transition: all 0.3s ease-in-out;
  animation: pulse 2s infinite ease-in-out;
}

@keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}

.big-button:hover {
  animation-play-state: paused;
}
</style>
