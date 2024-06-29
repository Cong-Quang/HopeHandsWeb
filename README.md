[FIlE backup Web wordpress](https://drive.google.com/file/d/1TIyZP19o78S78tGmqW1VJQ-AcBdiA8JU/view?usp=sharing)
![Ngân](img/ngan.jpg)
![Quang](img/Quang.jpg)

```javascript
if (!defined('WP_DEBUG')) {
    die('Direct access forbidden.');
}

add_action('wp_enqueue_scripts', function () {
    wp_enqueue_style('parent-style', get_template_directory_uri() . '/style.css');
});

/*
Thêm nút mua ngay và chat trực tiếp vào trang chi tiết sản phẩm Woocommerce
*/
add_action('woocommerce_after_add_to_cart_button', 'vuontainguyen_quickbuy_and_chat_button');
function vuontainguyen_quickbuy_and_chat_button() {
    global $product;
    ?>
    <style>
        .vuontainguyen-quickbuy {
            display: flex;
            justify-content: space-between;
            gap: 10px;
        }
        .vuontainguyen-quickbuy .button {
            flex: 1;
            margin-top: 10px;
            padding: 10px;
            text-align: center;
            border: none;
            cursor: pointer;
            color: white;
            font-weight: bold;
        }
        .vuontainguyen-quickbuy .chat_now_button {
            background-color: #0073aa;
        }
        .vuontainguyen-quickbuy .buy_now_button {
            background-color: #ff9900;
            color: white;
        }
        .vuontainguyen-quickbuy .button:hover {
            opacity: 0.9;
        }
    </style>
    <div class="vuontainguyen-quickbuy">
        <button type="button" class="button chat_now_button" onclick="window.location.href='https://www.facebook.com/profile.php?id=61560952961112'">
            <?php _e('Chat Ngay', 'vuontainguyen'); ?>
        </button>
        <button type="button" class="button buy_now_button">
            <?php _e('Mua ngay', 'vuontainguyen'); ?>
        </button>
    </div>
    <input type="hidden" name="is_buy_now" class="is_buy_now" value="0" autocomplete="off"/>
    <script>
        jQuery(function($){
            $('body').on('click', '.buy_now_button', function(e){
                e.preventDefault();
                var thisParent = $(this).closest('form.cart');
                if($('.single_add_to_cart_button', thisParent).hasClass('disabled')) {
                    $('.single_add_to_cart_button', thisParent).trigger('click');
                    // Wait for add-to-cart action to complete before redirecting
                    setTimeout(function(){
                        window.location.href = '<?php echo esc_url(wc_get_checkout_url()); ?>';
                    }, 1000); // Adjust timeout as needed (1 second here)
                    return false;
                }
                thisParent.addClass('vuontainguyen-quickbuy');
                $('.is_buy_now', thisParent).val('1');
                // Trigger add-to-cart action
                $('.single_add_to_cart_button', thisParent).trigger('click');
                // Wait for add-to-cart action to complete before redirecting
                setTimeout(function(){
                    window.location.href = '<?php echo esc_url(wc_get_checkout_url()); ?>';
                }, 1000); // Adjust timeout as needed (1 second here)
            });
        });
    </script>
    <?php
}

add_filter('woocommerce_add_to_cart_redirect', 'redirect_to_checkout_after_add_to_cart');
function redirect_to_checkout_after_add_to_cart($redirect_url) {
    if (isset($_REQUEST['is_buy_now']) && $_REQUEST['is_buy_now']) {
        $redirect_url = wc_get_checkout_url(); // Redirect to checkout for "Buy Now"
    }
    return $redirect_url;
}

```