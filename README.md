# [GoT books to series](got-books-to-series.surge.sh)

Designed by Alyssa Karla Mungcal<br>
Developed by Jocelyn Tan <br>
With help from Pooja

### Vertical Sankey
Code based on Ben Logan’s https://github.com/benlogan1981/VerticalSankey <br>
Data from Joel Geddert's http://joeltronics.github.io/got-book-show/bookshow.html

### Barcharts
Some text data from reading the books, <br>
Most from https://gameofthrones.fandom.com/wiki/Differences_between_books_and_TV_series<br>
<br>
Scene by scene timing and screenshots by Alyssa, Jocelyn and Pooja.

### How it is made
- Watch every episode and take screenshots with VLC, naming the images with S, E, and scene number
- In the excel, each season is its own file and each episode its own tab, with columns for timing of scene end, formula for scene duration, text for comparison and arbitrary assigning of rating.
- Each tab is saved as csv and converted to json online, and each image is saved as jpg and compressed to widths of 640px as container of site is 1200px.
- Description was stuck to the middle of screen for better scrolling experience
- Preloaded images of an episode on initial episode click, for smoother experience while navigating the barcharts.
- Added mobile images with width 420px for better loading on mobile sites using https://www.iloveimg.com/resize-image

### Promotion
Site was completed for the premiere of season 7, and Google Analytics added for tracking of user views. Promotion was done on Reddit, FlowingData, Facebook etc
<br>
Reddit: https://www.reddit.com/r/asoiaf/comments/bguiwn/spoilers_main_have_you_ever_wondered_how_the/
FlowingData: https://flowingdata.com/2019/05/06/game-of-thrones-books-versus-television-series/

Unique views by June 2019: 15,000+

### Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```
