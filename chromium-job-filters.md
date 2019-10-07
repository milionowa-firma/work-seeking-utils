
Portals promote certain offers, thus it is usually undesired to provide user with function to filter unwanted out. Yet, here is easy solution.

1. install [Chromium JS extension](https://chrome.google.com/webstore/detail/custom-javascript-for-web/ddbjnfjiigjmcpcpkmhogomapikjbjdk)
2. paste and modify below to filter out unwanted job offers (for now Glassdoor.com, nofluffjobs.pl, justjoin.it, pracuj.pl, linkedin.com/jobs/search


## Glassdoor.com

glassdoor.com

```javascript

var unwanted = ["Some", "Unwanted", "Companies"];

unwanted.forEach((o, i, a) => a[i] = a[i].replace("&", "&amp;"));

customjsReady(".mfp-bg mfp-ready", function(i){ $(this).hide(); }); // hide annoying popup

let item_class = "li.jl";
var hidden = [];
customjsReady(item_class, function( index ) {
    var row = $(this).find(".empLoc").html();
    var company = row.substring(6, row.indexOf("– <span class=")-1).trim();
    if ($.inArray(company, unwanted) != -1){
        $(this).hide();
        hidden.push(company);
    }
});
if (hidden.length > 0)
  setTimeout( function(){alert("Companies hidden: " + hidden.filter((v, i, a) => a.indexOf(v) === i))}, 1000 );
```

## NoFluffJobs.com

nofluffjobs.com

```javascript

var unwanted = ["Some", "Unwanted", "Companies"];
// example     ["IT Kontrakt", "ASTEK Polska", "CodiLime", "7N"];
var hidden = [];
let item_class = ".list-item";
customjsReady(item_class, function( index ) {
    var row = $(this).find(".posting-company").html();
    var company = row.substring(row.indexOf("@ ") + 2, row.indexOf("</span>"));
    if ($.inArray(company, unwanted) != -1){
        $(this).hide();
        hidden.push(company);
    }
});
alert("Companies hidden: " + hidden.filter((v, i, a) => a.indexOf(v) === i));

```

## JustJoin.it

justjoin.it

```javascript

// same like above but replace
let item_class = ".offer-item";

// and
  var row = $(this).find(".company-name");
  var company = $(row).text().trim().substr(1).trim();

```

## Pracuj.pl

pracuj.pl

```javascript

// same like above but replace
let item_class = "li.o-list_item";

// and
  var row = ""; // or remove line
  var company = $(this).find("h3").text().trim();

```


## Linkedin.com/jobs/search

linkedin.com/jobs/search

```javascript

// without jQuery for a change
var unwanted = ["Some", "Unwanted", "Companies"];
var hidden = [];
let item_class = "li.job-listing";
customjsReady(item_class, function( index ) {
    var company = index.getElementsByClassName("company-name-text")[0].innerText;
    unwanted.forEach(function(entry) {
      if (unwanted.indexOf(company) != -1 && index.parentElement){
        index.parentElement.removeChild(index);
        hidden.push(company);
      }
    });
});
if (hidden.length > 0)
  setTimeout( function(){ alert("Companies hidden: " + hidden.filter((v, i, a) => a.indexOf(v) === i))}, 1000 );

```

## todo: stackoverflow.com/jobs parser
## todo: zdalnie.io parser

## todo:
- parsers for aggregators: "JobsForGeek", "Crossweb", "JarJobs.com", "IT-Leaders_pl2018", "Bulldogjob" ( all of them publish also aggregated posts on wykop.pl )
