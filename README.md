# MageProfis_ShippingDetailsModal
Open shipping costs from the tax details (Inkl. 19% USt., zzgl. **Versandkosten**) in a modal instead of a new page.


### Javascript
```javascript
/* Open shipping details in modal */
jQuery("body").on("click", ".shipping-cost-details a", function (e) {
    e.preventDefault();
    
    jQuery('#shipping_costs_modal').modal('show');
    
    jQuery.ajax({
        url: jQuery(this).attr('href'),
        type: "post",
        dataType: "html",
        success: function (data) {
            var data = $(data).find('[role=main]');
            
            //remove modal
            data.find('#shipping_costs_modal').remove();
            
            //get title and remove
            var title = data.find('.page-title h1, .page-title h2, .page-title h3, .page-title h4, .page-title h5').text();
            data.find('.page-title').remove();
            
            jQuery('#shipping_costs_modal .modal-title').html( title );
            jQuery('#shipping_costs_modal .modal-body').html( data.html() );
        }
    });
});
```

### local.xml
```xml
<?xml version="1.0"?>
<layout>
    <default>        
        <reference name="content">
            <block type="core/template" name="shipping_costs.modal" after="-" template="mageprofis/shippingdetailsmodal/modal.phtml" />
        </reference>
    </default>
</layout>
```

### Template
mageprofis/shippingdetailsmodal/modal.phtml
```xml
<div class="modal fade" id="shipping_costs_modal" tabindex="-1" role="dialog">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title">Wird geladen...</h4>
      </div>
      <div class="modal-body">
        <p>Wird geladen...</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal"><?php echo $this->__('Close') ?></button>
      </div>
    </div><!-- /.modal-content -->
  </div><!-- /.modal-dialog -->
</div><!-- /.modal -->
```
