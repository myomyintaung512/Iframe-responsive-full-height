# Iframe Responsive Full Height
Responsive full height for iframe document

## Iframe Document
```html
<!-- you can remove this script link if you have already loaded jquery in your project -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <script type='text/javascript'>
        var sendMessage = function (msg) {
            // Make sure you are sending a string, and to stringify JSON
            window.parent.postMessage(msg, '*');
        };
        // sent body height to parent when DOM emelemt is ready
        // but Image height is not included yet. so it can be different with actual height
        jQuery(document).ready(function(){
          // sent document height to parent
          sendMessage(jQuery( 'body' ).innerHeight());

          // sent document height to parent when resize browser
          jQuery(window).on('resize',function() {
              sendMessage(jQuery( 'body' ).innerHeight());
          });
        });
        // sent document height to parent when iframe is fully loaded.
        // this stage all images height is added
        jQuery(window).load(function(){
          sendMessage(jQuery( 'body' ).innerHeight());
        });
    </script>
```

## Parent Document
```html
<!--
      must apply this css to iframe to solve IOS iframe width issue
      width: 1px; min-width: 100%; *width: 100%;
      -->
    <iframe id='myiframe' style="height: 100%; width: 1px; min-width: 100%; *width: 100%; border: 0 none transparent; display: block;" src="http://doamin.com/iframe.html" width="1" height="150" frameborder="0" scrolling="no"></iframe>

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <script type='text/javascript'>
        // addEventListener support for IE8
        function bindEvent(element, eventName, eventHandler) {
            if (element.addEventListener){
                element.addEventListener(eventName, eventHandler, false);
            } else if (element.attachEvent) {
                element.attachEvent('on' + eventName, eventHandler);
            }
        }
        // Listen to message from iframe document
        bindEvent(window, 'message', function (e) {
            // show iframe document height in #results div
            jQuery('#results').html(e.data);
            // adjust iframe height
            jQuery('#myiframe').css('height', e.data);
        });
    </script>
```
