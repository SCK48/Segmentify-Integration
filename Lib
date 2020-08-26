/* CUSTOMER_NAME */
/* Do not load Segmentify more than one to prevent potential error occurrence */
if (window['SegmentifyTrackingObject']) {
  throw new Error("Segmentify is already loaded!");
}

var segNamespace = "Segmentify";

window['SegmentifyTrackingObject'] = segNamespace;

window[segNamespace] = window[segNamespace] || function() {
  (window[segNamespace].q = window[segNamespace].q || []).push(arguments);
};

window[segNamespace].config = {
  // If the account registered into e-commerce machine uncomment first line, otherwise (for content websites) uncomment second one
  //segmentifyApiUrl: '//dce1.segmentify.com/',
  //segmentifyApiUrl: '//dcc2.segmentify.com/',
  //domain: 'domain.com'
};

/* Initialize Segmentify with your Api Key */
Segmentify('apikey', 'xxx');

function waitSegmentifyAndjQuery() {
  if (window["_SgmntfY_"] && window["_SgmntfY_"]._getJq()) {
    window.segJquery = window["_SgmntfY_"]._getJq();

    segJquery(document).ready(function() {
      SegmentifyIntegration(window.segJquery).init();
    });
  } else {
    setTimeout(waitSegmentifyAndjQuery, 100);
  }
}

var SegmentifyIntegration = function(jQuery) {
  var segmentifyEvents = {
    viewPage: function(category, subCategory) {
      /* console.log("Pageview Event is going", pageVariables.category, pageVariables.subCategory); */
      Segmentify('view:page', {
        'category': category,
        'subCategory': subCategory
      });
    },
    viewProduct: function(productObj) {
      /* console.log("Product View Event is going", productObj); */
      Segmentify('view:product', productObj);
    },
    checkoutBasket: function(basketObj) {
      /* console.log("Checkout Basket event is going", basketObj); */
      Segmentify('checkout:basket', basketObj);
    },
    checkoutPurchase: function(purchaseObj) {
      /* console.log("Checkout Purchase event is going", purchaseObj); */
      Segmentify('checkout:purchase', purchaseObj);
    },
    basketAdd: function(basketObj) {
      /* console.log("Basket Add Event is going", basketObj); */
      Segmentify('basket:add', basketObj);
    },
    basketRemove: function(basketObj) {
      /* console.log("Basket Remove Event is going", basketObj); */
      Segmentify('basket:remove', basketObj);
    },
    basketClear: function(basketObj) {
      /* console.log("Basket Clear Event is going", basketObj); */
      Segmentify('basket:clear', basketObj);
    },
    userUpdate: function(userObj) {
      /* console.log("User Update Event is going", userObj); */
      Segmentify('user:update', userObj);
    },
    userId: function(id) {
      /* console.log("User ID is going to be changed", id); */
      Segmentify('userid', id);
    },
    custom: function(customObj) {
      /* console.log("Custom Event is going", customObj); */
      Segmentify('event:custom', customObj);
    }
  };

  var helperFunctions = {
    "setCookie": function(cname, cvalue, exdays) {
      window["_SgmntfY_"]._storePersistentData(cname, cvalue, exdays, false);
    },
    "getCookie": function(cname) {
      return window["_SgmntfY_"]._getPersistentData(cname, false);
    },
    "getQueryParameter": function(pname, url) {
      return window["_SgmntfY_"]._getQueryParameter(pname, url);
    }
  };
  
  var pageVariables = {
    category: "",
    subCategory: ""
  };

  var findPageType = function() {
    try {
      /* Home Page, Category Page, Product Page, Basket Page, Search Page, Checkout Success Page */
      if (0) {
        pageVariables.category = "Home Page";
        return;
      }

      if (0) {
        pageVariables.category = "Category Page";
        pageVariables.subCategory = "";
        return;
      }

      if (0) {
        pageVariables.category = "Product Page";
        pageVariables.subCategory = "";
        return;
      }

      if (0) {
        pageVariables.category = "Basket Page";
        return;
      }

      if (0) {
        pageVariables.category = "Search Page";
        pageVariables.subCategory = "";
        return;
      }

      if (0) {
        pageVariables.category = "404 Page";
        return;
      }

      if (0) {
        pageVariables.category = "Purchase Success Page";
        return;
      }
    } catch (err) {
      window.segErr = err;
    }
  };

  var triggerPageFunction = function(category) {
    try {
      if (category && pageFunctions.hasOwnProperty(category)) {
        pageFunctions[category]();
      }

      pageFunctions["All Pages"]();
    } catch (err) {
      window.segErr = err;
    }
  };

  var init = function() {
    findPageType();
    triggerPageFunction(pageVariables.category);
  };

  var pageFunctions = {
    "All Pages": function() {
      segmentifyEvents.viewPage(pageVariables.category, pageVariables.subCategory);
    },
    "Home Page": function() {},
    "Category Page": function() {},
    "Product Page": function() {
      var productObj = {};

      // Gather information about the product
      productObj["brand"] = "";
      productObj["title"] = "";
      productObj["description"] = "";
      productObj["productId"] = "";
      productObj["image"] = "";
      productObj["price"] = "";
      productObj["oldPrice"] = "";
      productObj["inStock"] = false;
      productObj["productUrl"] = "";
      productObj["category"] = "";
      productObj["categories"] = [];
      productObj["params"] = {};

      // Send product view event
      segmentifyEvents.viewProduct(productObj);
    },
    "Search Page": function() {},
    "404 Page": function() {},
    "Basket Page": function() {
      var basketAmount = "";
      var basketProducts = [];

      // Put basket event information into a variable
      var basketInfo = {
        "totalPrice": basketAmount,
        "productList": basketProducts
      };

      // Send checkout basket event
      segmentifyEvents.checkoutBasket(basketInfo);
    },
    "Purchase Success Page": function() {
      var purchaseAmount = "";
      var purchaseProducts = [];
      var orderNo = "";

      // Put purchase event information into a variable
      var purchaseInfo = {
        "orderNo": orderNo,
        "totalPrice": purchaseAmount,
        "productList": purchaseProducts
      };

      // Send checkout purchase event
      segmentifyEvents.checkoutPurchase(purchaseInfo);
    }
  };

  return {
    init: init
  };
};

// Call Wait Function at the bottom of tne script
waitSegmentifyAndjQuery();
