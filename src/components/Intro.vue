<template>
  <div class="intro">
    <img src="title-logo.svg"/>
    <h1>Books versus TV series</h1>
    <p class="deck">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc magna erat, viverra in convallis nec, tempor a justo. Aliquam euismod orci vitae nisi sodales faucibus. In consequat lobortis nisi at gravida. Praesent rutrum felis non turpis vulputate vestibulum. Vestibulum quis neque eu elit fringilla tincidunt. Aliquam neque mi, tempor finibus nisl eget, fringilla sagittis orci. Nulla molestie ultrices malesuada. Morbi mollis sem eget velit congue, quis ultrices augue mattis. Maecenas non velit semper orci dignissim dapibus. Donec quis neque a nunc aliquam varius. Nullam vitae sollicitudin sapien, nec elementum mauris. Curabitur quis sagittis nibh, in commodo est. Vestibulum et quam quis est cursus placerat in elementum arcu. Donec dapibus eu nunc nec congue.
    </p>
    <p class="produced">Produced By: <a href="https://www.behance.net/makuLhaiM">Alyssa Karla Mungcal</a>, <a href="http://webdev.jocelyn-tan.com/">Jocelyn Tan</a> and Pooja Sharma | Published: 15 April 2019</p>
  </div>
</template>

<style lang="scss">
.intro {
  max-width: 700px;
  margin: 0 auto;
  padding: 30px 15px;

  img {
    width: 50%;
  }

  h1 {
    font-family: 'Lora', serif;
    font-size: 48px;
    line-height: 1.3em;
    color: #E1EDF4;
    margin: 0px 0 20px;

    @media (max-width: 480px){
      font-size: 35px;
      max-width: 250px;
    }
  }
  p.deck {
    font-family: 'PT Sans', sans-serif;
    font-size: 15px;
    line-height: 1.3em;
    color: #E1EDF4;
  }

  p.produced {
    font-family: 'PT Sans', sans-serif;
    text-transform: uppercase;
    font-size: 12px;
    line-height: 1.3em;
    color: rgba(#E1EDF4, 0.8);
  }
}
</style>
