**Google Analytics PLT** plugin generates the basket form required for
Product Level Tracking if the client has Google Analytics datalayer
populated with transaction data (Enhanced Ecommerce)
<https://developers.google.com/tag-manager/enhanced-ecommerce#purchases>

# Supported Pages

- Checkout Page

# Configuration

Plugin does not require configuration. AWIN.Tracking.Sale object and
Google Analytics datalayer populated with transaction data (Enhanced
Ecommerce)
<https://developers.google.com/tag-manager/enhanced-ecommerce#purchases>
must be implemented on the checkout page.

# Plugin Source Code


``` javascript
(function () {
    var createProductForm = function() {
        var filteredProducts = dataLayer.filter(function (x) {return x.ecommerce;});
        if (filteredProducts[0]
            && filteredProducts[0].ecommerce
            && filteredProducts[0].ecommerce.purchase
            && filteredProducts[0].ecommerce.purchase.products) {
            var products = filteredProducts[0].ecommerce.purchase.products;

            var rows = [];
            var merchant = AWIN.Tracking.iMerchantId;
            for (var i = 0; i < products.length; i++) {
                rows.push([
                    "AW:P",
                    (merchant ? merchant.toString() : ""),
                    AWIN.Tracking.Sale.orderRef,
                    products[i].id,
                    products[i].name,
                    products[i].price,
                    products[i].quantity,
                    products[i].id,
                    "DEFAULT",
                    products[i].category
                ].join("|"));
            }
            AWIN.Tracking.Sale.plt = rows.join("\n");
            var basketTextArea = document.createElement('textarea');
            basketTextArea.setAttribute('wrap', 'physical');
            basketTextArea.setAttribute('id', 'aw_basket');
            basketTextArea.innerHTML = AWIN.Tracking.Sale.plt;

            var basketForm = document.createElement('form');
            basketForm.setAttribute('style', 'display:none');
            basketForm.setAttribute('name', 'basket_form');
            basketForm.appendChild(basketTextArea);
            document.getElementsByTagName('body')[0].appendChild(basketForm);
        }
    };

    if (AWIN.Tracking.Sale) {
        createProductForm();
    }
})();
```

