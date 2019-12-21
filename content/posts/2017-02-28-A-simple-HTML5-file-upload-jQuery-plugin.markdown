---
layout: post
title:  "A simple HTML5 file upload jQuery plugin"
date:   2017-02-28
categories: ['web development']
tags: ['javascript']
---

```js
;(function($) {
  $.fn.html5upload = function(options) {
    var cfgs = $.extend({
      url: '',
      tmpl: '',
      uploadBtn: '',
      previewContainer: '',
      multiple: false,
      onProgress: null,
      onSuccess: null,
      onError: null
    }, options);

    var $el = $(this);
    var $uploadBtn = $(cfgs.uploadBtn);
    var $progressBar = $(cfgs.progressBar);
    var $previewContainer = $(cfgs.previewContainer);
    var datas = [];
    var xhrs = [];
    var uploadIndex = 0;
    var tmpl = cfgs.tmpl || '<li class="weui-uploader__file" data-upload-index="#index#" style="background-image:url(#url#)"><span class="ui-progress"></span><span class="ui-cancel"></span></li>';

    $el.on('change', function(e) {
      var url = window.URL || window.webkitURL || window.mozURL;
      var files = e.target.files;

      $.each(files, function(i, file) {
        var src;
        var newTmpl = tmpl;

        uploadIndex++;
        file.uploadIndex = uploadIndex;
        datas.push(file);

        if (url) {
          src = url.createObjectURL(file);
        } else {
          src = e.target.result;
        }

        if (!cfgs.multiple) {
          $previewContainer.css('background-image', 'url(' + src + ')');
        } else {
          newTmpl = newTmpl.replace('#url#', src).replace('#index#', file.uploadIndex);
          $previewContainer.append($(newTmpl));
        }
      });
    });

    $uploadBtn.on('click', function() {
      var countSuccess = 0;
      var countError = 0;
      var total = datas.length;

      if (datas.length > 0) {
        $uploadBtn.prop('disabled', true).addClass('disabled');
      }

      $.each(datas, function(i, file) {
        var data = new FormData();
        var uploadIndex = file.uploadIndex;
        var $preview = $previewContainer.find('li[data-upload-index=' + uploadIndex + ']');

        data.append(file.name ? file.name : 'file-' + i, file);

        var currentXhr = $.ajax({
          url: cfgs.url,
          data: data,
          cache: false,
          contentType: false,
          processData: false,
          type: 'POST',
          success: function(data) {
            if (typeof cfgs.onSuccess === 'function') {
              cfgs.onSuccess(file, data);
            } else {
              console.log(file.name, data);
            }

            countSuccess++;
            datas = removeElement(datas, uploadIndex, 'uploadIndex');
          },
          error: function(jqXHR, textStatus, errorThrown) {
            if (typeof cfgs.onError === 'function') {
              cfgs.onError(file, textStatus);
            } else {
              console.log(file.name, textStatus);
            }

            countError++;
          },
          complete: function() {
            if (total === countSuccess + countError) {
              $uploadBtn.prop('disabled', false).removeClass('disabled');
              xhrs = [];
            }
          },
          xhr: function() {
            var xhr = $.ajaxSettings.xhr();

            if (xhr.upload) {
              xhr.upload.addEventListener('progress', function(e) {
                if (e.lengthComputable) {
                  if (typeof cfgs.onProgress === 'function') {
                    cfgs.onProgress(file, e.loaded, e.total);
                  } else {
                    $preview.find('.ui-progress').animate({
                      width: parseInt((e.loaded / e.total) * 100, 10) + '%'
                    });
                    console.log(file.name, e.loaded, e.total);
                  }
                }
              }, false);
            }

            return xhr;
          }
        });

        xhrs.push({
          xhr: currentXhr,
          index: uploadIndex
        });
      });
    });

    $previewContainer.on('click', 'li .ui-cancel', function() {
      var index = parseInt($(this).parent('li').remove().data('upload-index'), 10);
      datas = removeElement(datas, index, 'uploadIndex');

      $.each(xhrs, function(i, xhr) {
        if (xhr.index === index) {
          xhr.xhr.abort();
          return false;
        }
      });
    });

    return this;
  }

  function removeElement(arr, value, prop) {
    var rest = arr.slice();

    for (var i = 0; i < rest.length; i++) {
      if (prop && rest[i][prop] === value || !prop && rest[i] === value) {
        rest.splice(i, 1);
        break;
      }
    }

    return rest;
  }
})(jQuery);
```
