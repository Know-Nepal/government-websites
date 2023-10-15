<template>
    <div class="government-website">
      <div class="icon-container">
        <img class="icon" src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/23/Emblem_of_Nepal.svg/1200px-Emblem_of_Nepal.svg.png" alt="Nepal Emblem" />
      </div>
      <h2>{{ website.name }}</h2>
      <p>{{ website.description }}</p>
      <a :href="website.url" target="_blank">Visit Website</a>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      website: {
        type: Object,
        required: true,
      },
    },
  };
  </script>
  
  
  <style scoped>
  .government-website {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 10px;
    border: 1px solid #4caf50;
    border-radius: 8px;
    width: 220px;
    margin: 10px;
    background-color: #ffffff;
    transition: all 0.3s ease;
  }
  
  .government-website:hover {
    box-shadow: 0px 0px 10px 0px #4caf50;
  }
  
  .icon-container {
    padding: 8px;
    border-radius: 50%;
    margin-bottom: 10px;
  }
  
  .icon {
    width: 50px;
    height: 50px;
  }
  
  h2 {
    font-size: 18px;
    margin-bottom: 8px;
  }
  
  p {
    font-size: 14px;
    margin-bottom: 10px;
  }
  
  a {
    text-decoration: none;
    color: #4caf50;
    font-weight: bold;
    transition: color 0.3s ease;
  }
  
  a:hover {
    color: #333;
  }
  </style>
  