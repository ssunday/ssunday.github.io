---
title: The Power of Stencil Templates
description: Reducing hard-coded HTML with Stencil
date: 4/4/2016
---

In my web tic tac toe Clojure app, I had been originally hardcoding in HTML and other things within the stencil/mustache file and a  for things like the board and settings page. The board was especially hard-coded. To display the game board I was assembling strings of HTML together in a presenter file that I had Stencil render as HTML. The settings page was also bulky because I had every A-Z marker typed out. It was pretty atrocious.

Thankfully, there existed a way to remove all this waste. And that way was to actually use Stencil to its fullest extent. Gasp. Stencil has ways to iterate through maps and to essentially create if/else blocks. Using this, I transformed the board table into this (pretend it is double bracket'd):

```mustache
<table class="centered">
  {#board}
    {#start-row}
    <tr>
    {/start-row}
    <td>
    {#current-player-is-ai}
      <h5>{value}</h5>
    {/current-player-is-ai}
    {^current-player-is-ai}
      {#open}}
        <input name="spot" type="radio" id={value} value ={value} checked/>
        <label for={value}></label>
      {/open}
      {^open}
        <h5>{{value}}</h5>
      {/open}
    {/current-player-is-ai}
    </td>
    {#end-row}
    </tr>
    {/end-row}
  {/board}}
</table>
```

The board presenter class now merely creates the map that has all the values (save the `current-player-is-ai` one) that Stencil uses to decide whether to display a static board value or to create an input field. All the custom CSS and HTML styling is done in the mustache file now.

As for the settings page, it *really* took advantage of Stencil's flexibility. Instead of having the A-Z input fields hard-coded in, they were generated in a presenter file using chars:

```clojure
(defn- get-A-Z-char []
  (map char (range (int \A) (inc (int \Z)))))

(defn markers-map [selected-marker]
  (let [A-Z (get-A-Z-char)]
    (map #(zipmap [:character :selected] [% (is-selected (.charAt selected-marker 0) %)]) A-Z)))
```

Then the actual mustache file utilizes this in a relatively compact way:

```mustache
<select class="browser-default" name="player-one-marker">
  {#markers-player-one}
    {#selected}
      <option value={character} selected>{character}</option>
    {/selected}
    {^selected}
      <option value={character}>{character}</option>
    {/selected}}
  {/markers-player-one}
</select>
```
It is a much needed improvement. It also allows the ability to have a particular markers default selected instead of always X/O. I had to do this anyway to add the feature of having the settings page be defaulted to whatever the settings were on the last successful submit.

The scores Mustache file was also tweaked to use templates, as it really improved the layout.

So. Conclusion: Stencil/Mustache is very powerful at reducing duplication. It removes the need for long, chaotic presenter functions that hard-code HTML. It made displaying information much easier. I probably should have looked at what it could do before hard coding anything.
