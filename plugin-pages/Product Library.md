
# Introduction

This page explains how to use the product javascript library to build a
customised product tag for a particular merchant. This tag setup is done
via the site2 tag management form explained below.
=AVOID BREAKING STUFF= Please be **aware** that any javascript errors in
the product scraper code may break tracking, so it's important to ensure
that they don't happen. Bare in mind that the code will be run on every
page on the merchant's site, not just product pages, and also that the
structure of product pages may change.

## Check that values are valid before using them

Don't assume that an element will be found, even when using the
AWIN.Tracking Library
**Bad:**


``` javascript
AWIN.Tracking.getElements({attribName: "id", attribValue: "sku"})[0];
```


**Good:**


``` javascript
var els = AWIN.Tracking.getElements({attribName: "id", attribValue: "sku"});
if (els.length > 0) {
  // Do something
}
```





## Avoid direct DOM manipulation because implementations vary across browsers

In general you should avoid anything that is a browser specific way of
doing something and use the AWIN.Tracking libraries. for example this is
not supported by all browsers.

**Bad:**


``` javascript
var els = document.getElementsByClassName('sku');
```



**Good:**


``` javascript
var els = AWIN.Tracking.getElements({attribName: "class", attribValue: "sku"});
```




# Tag Plugin

|               |                                         |
|:-------------:|:---------------------------------------:|
| Plugin Type:  |             Product Library             |
| Plugin Setup: | code to set AWIN.Tracking.ProductGetter |
|    Active:    |                   Yes                   |



=Product JavaScript Library=

## AWIN.Tracking.getQueryStringVariable (name)

- Get the value of a variable from the URL query string of the current
  document.
  Eg, on the page <http://foo.com?bar=1>,
  ``` javascript
  AWIN.Tracking.getQueryStringVariable('bar')
  ```

  will return '1'.


==AWIN.Tracking.getElements(selector, dom)==

- Returns an array of elements identified by the set of selector
  options.
  {object} selector - Selectors used to filter HTML elements. Requires
  at least one of the following attributes to be set:
  - *attribName* - A HTML attribute type to search for. **Required**
  - *attribValue* - The value of the attribute. Can be a string or a
    regular expression. **Required**
  - *tag* - A HTML tag type. Optional
- {object} dom HTMLElement - Only search descendants of this element.


==AWIN.Tracking.getAttribute(element, name)==

- Return the value of the named attribute on the element, or null if not
  set.
  Eg for
  ``` javascript
  <div class="foo"></div>
  ```

  ``` javascript
  AWIN.Tracking.getAttribute(element, 'class');
  ```

  will return 'foo';


==AWIN.Tracking.getTextContent(element)==

- Return the trimmed text content of the element.
  Eg for
  ``` javascript
  <div>1234</div>
  ```

  ``` javascript
  AWIN.Tracking.getTextContent(element);
  ```

  will return '1234';


==AWIN.Tracking.extractWithRegExp(str, pattern)==

- Used to extract part of a string with a regular expression. Will
  return the full matching part of the regular expression or the first
  group (if any).


**Extract full match**

- extractWithRegExp**('foo-834', /\d+/);** will return 834.


**Extract group match**

- extractWithRegExp**('4845-foo-7592', /^\d+-\w+-(\d+)\$/);** will
  return 7592.


==AWIN.Tracking.readHProduct()== Returns an object containing the
hProduct microformat values from the page. Will only extract the id,
name, and categories values. Returns null if there are no hProduct data
is present.
For more information about hProduct Microformat, please see the
following link; <http://microformats.org/wiki/hproduct>

# Examples

## From A JavaScript Variable

Product ID has already been set in JavaScript


``` javascript
<script type="text/javascript">
 productId = "12345";
</script>
```





``` javascript
AWIN.Tracking.ProductGetter = function() {
  if (typeof(productId) == 'undefined') {
    return null;
  }
  return {
    id: productId
  };
};
```



==From A Javascript dataLayer Variable (i.e. Google Tag Manager)==


``` javascript
<script>
  dataLayer = [];
  dataLayer.push({'customerId': ''});
  dataLayer.push({'customerTitle': ''});
  dataLayer.push({'customerFirstName': ''});
  dataLayer.push({'customerLastName': ''});
  dataLayer.push({'customerEmail': ''});
    dataLayer.push({'basketCount': 0});
  dataLayer.push({'basketProducts': [
        ]});
  dataLayer.push({'basketTotal': 0.00});
  dataLayer.push({'productSKU': 'bj4102'});
</script>
```





``` javascript
AWIN.Tracking.ProductGetter = function() {
    if (typeof dataLayer == "object") {
        for (var i = 0; i < dataLayer.length; i++) {
            if (typeof dataLayer[i].productSKU != "undefined") {
                return {
                    id: dataLayer[i].productSKU
                };
            }
        }
    }
    return null;
};
```



Here productSKU is \[8\] in the array, but the code will cycle through
the entire array until it finds productSKU. This makes it more robust
should further variables be added to the array by the merchant.


==Query String Variable== URL is
<http://www.foo.com/product?product_id=1234>.


``` javascript
AWIN.Tracking.ProductGetter = function() {
  var productId = AWIN.Tracking.getQueryStringVariable('product_id');
  if (!productId) {
    return null;
  }
  return {
    id: productId
  };
}
```



==From URL with regexp== URL is <http://www.foo.com/product/blah_1234>.


``` javascript
AWIN.Tracking.ProductGetter = function() {
  var productId = AWIN.Tracking.extractWithRegExp(document.location.href,/product\/[a-z]+_(\d+)/);
  if (!productId) {
    return null;
  }
  return {
    id: productId
  };
};
```



==Element With A Unique ID== Product ID is in an input element that has
a unique id and is in the attribute value.


``` javascript
<input type="hidden" name="sku" id="sku" value="12345"/>
```



\*Get the element that has the id of 'sku'

- Set the product ID to the whatever is stored in the attribute 'value'




``` javascript
AWIN.Tracking.ProductGetter = function() {
  var els = AWIN.Tracking.getElements({attribName: "id", attribValue: "sku"});
  if (els.length == 0) {
    return null;
  }
  var val = AWIN.Tracking.getAttribute(els[0], "value");
  if (!val) {
    return null;
  }
  return {
    id: val
  };
};
```



==Element By Type And Attribute== Product ID is in a meta tag in the
attribute content, but isn't identified by a unique id attribute


``` javascript
<meta name="productNumber" value="12345" />
```



\*Get the element that has the name of 'productNumber' and is a tag of
type meta

- Set the product ID to the whatever is stored in the attribute
  'content'




``` javascript
AWIN.Tracking.ProductGetter = function() {
  var els = AWIN.Tracking.getElements({attribName: "name", attribValue: "productNumber", tag: "meta"});
  if (els.length == 0) {
    return null;
  }
  var val = AWIN.Tracking.getAttribute(els[0], "value");
  if (!val) {
    return null;
  }
  return {
    id: val
  };
};
```



==Descendant Element== Product ID is in a generic HTML element with no
unique identifiers, but is the descendant of an element that **does**
have a unique identifier.


``` javascript
<div id="productInfo">
  This is a : <span name="description" value="Foo Widget">Foo Widget</span>
  <input type="hidden" id="productId" value="12345" />
<div id="relatedProduct">
  You might also like : <span name="description" value="Bar Widget">Bar Widget</span>
  <input type="hidden" id="productInfo" value="54321" />
```



\*Get the element that has the id of 'productInfo'

- Get the element that has the name attribute of 'productId', is an
  input, and is a descendant the element we just retrieved
- Set the product ID to the whatever is stored in the attribute 'value'




``` javascript
AWIN.Tracking.ProductGetter = function() {
  var par = AWIN.Tracking.getElements({attribName: "id", attribValue: "productInfo"});
  if (par.length == 0) {
    return null;
  }
  var els = AWIN.Tracking.getElements({attribName: "name", attribValue: "productId", tag:"input"}, par[0]);
  if (els.length == 0) {
    return null;
  }
  var val = AWIN.Tracking.getAttribute(els[0], "value");
  if (!val) {
    return null;
  }
  return {
    id: val
  };
};
```



==Regular Expression Extraction== Product ID is in an HTML element, but
with extra information in the value.


``` javascript
<input type="hidden" id="productInfo" value="category_54321_product_12345"/>
```



\*Get the element that has the id of 'productInfo'

- Extract the product ID from the "value" attribute with a Regular
  Expression




``` javascript
AWIN.Tracking.ProductGetter = function() {
  var els = AWIN.Tracking.getElements({attribName: "id", attribValue: "productInfo"});
  if (els.length == 0) {
    return null;
  }
  var val = AWIN.Tracking.getAttribute(els[0], "value");
  if (!val) {
    return null;
  };
  var match = AWIN.Tracking.extractWithRegExp(val, /^category_\d+_product_(\d+)$/);
  if (!match) {
    return null;
  }
  return {
    id: match
  };
};
```



==Element Has Different Names== Product ID is in an HTML element, but
the name may change slightly over different pages


``` javascript
<input type="hidden" id="foo_productInfo" value="12345"/>
```



``` javascript
<input type="hidden" id="bar_productInfo" value="12345"/>
```



\*Search for an element that has an id element matching a Regular
Expression

- Extract the product ID from the "value" attribute




``` javascript
AWIN.Tracking.ProductGetter = function() {
  var els = AWIN.Tracking.getElements({attribName: "id", attribValue: /^\w+_productInfo/});
  if (els.length == 0) {
    return null;
  }
  var val = AWIN.Tracking.getAttribute(els[0], "value");
  if (!val) {
    return null;
  };
  return {
    id: val
  };
};
```



==Extract Element Content== The product ID is in the text content of an
HTML element.


``` javascript
<span id="product_id">1234</span>
```





``` javascript
AWIN.Tracking.ProductGetter = function () {
  var els = AWIN.Tracking.getElements({attribName: "id", attribValue: "product_id"});
  if (els.length == 0) {
    return null;
  }
  return {
    id: AWIN.Tracking.getTextContent(els[0])
  };
};
```




## Page has hProduct data

Product information is stored in the hProduct microformat


``` javascript
<div class="hproduct">
  <h2 class="fn">Foo Widget</h2>
  <h3 class="price"><span class="money">£<span class="amount">12.34</span></span></h3>
  <span class="identifier">12345</span>
  <span class="category">Widgets</span>
```



\* Extract the hProduct data from the page


``` javascript
AWIN.Tracking.ProductGetter = function() {
  return AWIN.Tracking.readHProduct();
};
```



==Element doesn't have name combined with reg expression==


``` javascript
<form id="product_addtocart_form">
<div class="no-display">
            <input type="hidden" name="product" value="2403" />
            <input type="hidden" name="related_product" id="related-products-field" value="" />
<div class="product-name"><h1>Silent Night King Size Electric Blanket</h1></div><p>Product Code: 20.9035</p>
</form>
```



\*Get the parent element

- Get the child element by using childNodes
- Perform a regex on the childnode to get the id




``` javascript
AWIN.Tracking.ProductGetter = function () {
  var els = AWIN.Tracking.getElements({attribName: "id", attribValue: "product_addtocart_form"});

  if (els.length == 0) {
    return null;
  };
var child = AWIN.Tracking.getTextContent(els[0].childNodes[4]);

var match = AWIN.Tracking.extractWithRegExp(child,/^Product Code: (.+)$/);
if (!match) {
  return null;
}
return {
  id: match
};

}
```



=Tests= Before making changes on live please test your product getter
code on the merchant site first using FireBug.

- visit a product page on merchant website in firefox
- open FireBug and make sure the console is enabled
- copy the code below and replace PRODUCT_GETTER_CODE with your actual
  code
- click run, check console for message




``` javascript
PRODUCT_GETTER_CODE

if (typeof(AWIN.Tracking.Product) === 'undefined') {
    AWIN.Tracking.scriptAppend("https://www.awin1.com/awin.product.js");
    console.log("fetched product plugin, click 'Run' again");
} else {
    console.log('Product ID found: ' + AWIN.Tracking.Product.id);
}
```

