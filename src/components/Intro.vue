<template>
  <div class="intro">
    <img src="title-logo.svg"/>
    <h1>Books versus TV series</h1>
    <p class="deck">As we embark on the epic final season, most of us know that the TV series has already exceeded the storyline of the (released) books. Find out how much of the previous seasons actually follow the books and how much have been changed.
    </p>
    <p class="produced">Produced By: <a href="https://www.behance.net/makuLhaiM">Alyssa Karla Mungcal</a>, <a href="http://webdev.jocelyn-tan.com/">Jocelyn Tan</a> and Pooja Sharma | Published: 15 April 2019</p>
    <div class="paragraphs">
      <p>There are various reasons why the screen version would differ from the book, one of which is the limited screen time, but most important reason is the budget. Every actor costs money, and more if they are speaking roles, so sometimes a minor character’s action is given to an existing character. The direwolves are shown more in the books, but they cost money to animate, unless you would see less of the dragons.
      </p>
      <p>The below Sankey diagram shows how much of each book is used as material for each season. We quantified it by counting the number of chapters that are shown in a particular season. Each chapter in the books is told from the point of view (POV) of a character. As you can see, the first season follows the first book quite closely, and the relationship decreases every following season.
      </p>
    </div>
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
    font-size: 18px;
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

  a {
    color: #AFC9F5;

    &:visited {
      color: #404E86;
    }
  }

  .paragraphs {
    margin: 80px 0 30px;

    p {
      font-family: 'PT Sans', sans-serif;
      font-size: 15px;
      line-height: 1.3em;
      color: #E1EDF4;
    }
  }
}
</style>
