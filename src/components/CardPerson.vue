<template>
  <div class="person_card">
    <div class="person_img">
      <img :src="img" />
    </div>
    <div class="person_info">
      <div class="person_name">
        <h2>{{ name }}</h2>
        <span>{{ status }}</span>
      </div>
      <div class="person_location">
        <span class="person_subtitle">Last know location:</span>
        <p>{{ location }}</p>
      </div>
      <div class="person_seen">
        <span class="person_subtitle">First seen in:</span>
        <p>{{ seen }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    url_img: String,
    name: String,
    location: String,
    seen: String,
    status: String,
    img: String,
  },
};
</script>

<style>
.person_card {
  display: flex;
  background-color: rgb(60, 62, 68);
  border-radius: 0.5rem;
  overflow: hidden;
  gap: 15px;
  width: 600px;
  height: 220px;
  margin: 0.2rem;
}
.person_info {
  display: flex;
  flex: 3 1 0%;
  flex-direction: column;
  justify-content: center;
  gap: 10px;
}
.person_name {
  color: #ffff;
  font-weight: bold;
}
.person_location {
}
.person_seen {
}
.person_subtitle {
  color: rgb(158, 158, 158);
}
p {
  color: #ffff;
  cursor: pointer;
  transition: 0.3s;
}
p:hover {
  color: rgb(255, 152, 0);
}
.person_img {
  flex: 2 1 0%;
  width: 100%;
}
.person_img img {
  width: 100%;
  height: 100%;
  margin: 0px;
  opacity: 1;
  transition: opacity 0.5s ease 0s;
  object-position: center center;
  object-fit: cover;
}
@media (width < 650px) {
  .person_card {
    flex-direction: column;
    height: initial;
  }
  .person_info {
    padding: 1rem;
  }
}
</style>
