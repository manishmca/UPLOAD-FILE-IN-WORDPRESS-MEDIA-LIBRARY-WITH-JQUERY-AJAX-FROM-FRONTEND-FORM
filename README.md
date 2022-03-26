# UPLOAD-FILE-IN-WORDPRESS-MEDIA-LIBRARY-WITH-JQUERY-AJAX-FROM-FRONTEND-FORM

<form method="post">
<input type="file" id="user-file">
<input type="submit" name="Submit" id ="ajax_btn">
</form>


/** ajax code footer.php  **/
<script>
jQuery(document).ready(function(){
jQuery('#ajax_btn').click(function(event){
event.preventDefault();
var ajaxurl = '<?php echo admin_url('admin-ajax.php'); ?>';
var formData = new FormData();
formData.append('updoc', jQuery('input[type=file]')[0].files[0]);
formData.append('action', "submit_ajax_data");
jQuery.ajax({
url: ajaxurl,
type: 'POST',
data:formData,cache: false,
processData: false, // Don’t process the files
contentType: false, // Set content type to false as jQuery will tell the server its a query string request
success:function(data) {
alert(data);


 
},

});

});
});
</script>



add_action( 'wp_ajax_submit_ajax_data', 'submit_ajax_data_update');
add_action('wp_ajax_nopriv_submit_ajax_data', 'submit_ajax_data_update' );
function submit_ajax_data_update() {
if ( $_FILES ) {  
require_once(ABSPATH . "wp-admin" . '/includes/image.php');
require_once(ABSPATH . "wp-admin" . '/includes/file.php');
require_once(ABSPATH . "wp-admin" . '/includes/media.php');
 $file_handler = 'docfile';
  echo $attach_id = media_handle_upload($file_handler,$pid );		
}
wp_die();
}
