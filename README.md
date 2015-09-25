<img src="http://stephaneadamgarnier.com/prompt/assets/code.png" align="" height="48" width="48">

<a target="_blank" href="http://stephaneadamgarnier.com/prompt/stagPrompt.html">Demo</a>
# Prompt
replacement to the 'prompt()' javascript call that provides multiple fields while looking-like as closely as possible to browsers'native style  ( used on Ubuntu 14.04, only Fireworks css has been added, but should work fine cross-browsers, since not using any browser-vendor specific implms )

Also, it uses some trickety hacks allowingto to change stuff that shouldn't be using the following css helpers
```javascript
// ( .. )

// usage: Typer.cssRuleIndexFromSelector('input[name="promptSettings_color"]::-moz-placeholder')
// or better: Typer.cssRuleIndexFromSelector('input.dynamic[name="promptSettings_color"]::-moz-placeholder')
cssRuleIndexFromSelector: function (selectorText){
  for(var i = 0; i <= document.styleSheets[0].cssRules.length; i++){
    try{ 
      if( document.styleSheets[0].cssRules[i].selectorText == selectorText ) {
        //console.log(document.styleSheets[0].cssRules[i].cssText);
        return i;
      }
    } catch(e) { return -1; } 
  }
},
    
// remove a CSS rule by specifying it's selector - R: supports pseudo selectors ;)
// other helper consumed by the above ( should realy be included in the spec as it's possible to do so :/ .. were they tired of writing useful fcns ? .. )
// usage: Typer.removeCssRule('input[name="promptSettings_color"]::-moz-placeholder');
// or better: Typer.removeCssRule('input.dynamic[name="promptSettings_color"]::-moz-placeholder');
removeCssRule: function (selectorText){
  // checks if the selector actually exist ( if the returned id is different than '-1' )
  var ruleId = this.cssRuleIndexFromSelector(selectorText); // ex: 'input[name="promptSettings_color"]::-moz-placeholder'
  // remove the rule which has it's i dassociated to that selector
  if( ruleId != -1 ) document.styleSheets[0].deleteRule( ruleId ); // nb: could improve code a littl' bit by looking at EVERY stylesheet instead of just 1st one ( R: having most concat'd is better )
},

// add an entire CSS rule ( aka, specify properties within ) specifying it's selector - R: supports pseudo selectors ;)
// usage: usage: Typer.addCssRule('input[name="promptSettings_color"]::-moz-placeholder', '{ color: green !important; }')
// or better: usage: Typer.addCssRule('input.dynamic[name="promptSettings_color"]::-moz-placeholder', '{ color: green !important; }')
addCssRule: function(selectorText, cssRule){
  document.styleSheets[0].insertRule(selectorText + cssRule, 0);
}

// ( .. )
```

<img src="http://stephaneadamgarnier.com/prompt/assets/prompt.png" align="" height="" width="100%">
