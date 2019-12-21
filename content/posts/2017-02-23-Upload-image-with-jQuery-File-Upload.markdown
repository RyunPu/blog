---
layout: post
title:  "Upload image with jQuery-File-Upload"
date:   2017-02-23
categories: ['web development']
tags: ['javascript']
---

```js
export default {
  init(selector, options = {}) {
    let datas = [];
    let uploading = false;
    let myindex = 0;

    const self = this;
    const container = $(selector);
    const fileInput = container.find('input[type=file]');
    const uploadBtn = container.find('.btn-upload');
    const uploadTpl = container.find('.template-upload');

    self.cfgs = $.extend({
      url: '',
      autoUpload: false,
      accept: /^image\/(gif|jpe?g|png)$/i,
      maxFileSize: 0,
      add(e, data) {
        if (data.files && data.files[0]) {
          const tpl = '';
          const file = data.files[0];
          console.log('add', file);

          myindex++;
          data.myindex = myindex;

          if (!self.cfgs.accept.test(file.type)) {
            console.log('部分文件不符合格式，已自动过滤');
            return;
          }

          if (self.cfgs.maxFileSize !== 0 && file.size > self.cfgs.maxFileSize) {
            console.log('部分文件过大，已自动过滤');
            return;
          }

          tpl = `
                <div class="col-sm-3 col-xs-6" data-index=${myindex}>
                  <div class="content" style="background-image: url(${URL.createObjectURL(file)})">
                    <i class="glyphicon glyphicon-trash"></i>
                    <p class="name">${file.name}</p>
                    <p class="tt-progress"><span></span></p>
                    <span class="size"></span>
                    <span class="done"></span>
                    <div class="error">
                      <span class="msg">上传失败</span>
                      <span class="icon"></span>
                    </div>
                  </div>
                </div>
                `;

          template.append(tpl);
          datas.push(data);
        }
      },
      progress(e, data) {
        console.log('progress', data);

        let loaded = parseInt(data.loaded / 1024) + 'KB';
        let total = parseInt(data.total / 1024) + 'KB';

        container.find('[data-index=' + data.myindex + '] .tt-progress span').css({
          display: 'block',
          width: data.loaded / data.total * 100 + '%'
        });

        if (data.total >= 1048576) {
          loaded = parseInt(data.loaded / 1048576) + 'MB';
          total = parseInt(data.total / 1048576) + 'MB';
        }

        container.find('[data-index=' + data.myindex + '] .size').html(loaded + '/' + total);
      },
      change(e, data) {
        console.log('change', data);

        if (!uploading) {
          self.enableBtn(uploadBtn, '开始上传');
        }
      },
      start(e) {
        console.log('start', data);

        container.find('.error').hide();
        self.disableBtn(uploadBtn, '上传中...');
        uploading = true;
      },
      stop(e) {
        console.log('stop', data);

        if (datas.length) {
          self.enableBtn(uploadBtn, '开始上传');
        } else {
          self.disableBtn(uploadBtn, '开始上传');
        }

        uploading = false;
      },
      fail(e, data) {
        console.log('fail', data);

        self.showError(container, data);
      },
      done(e, data) {
        console.log('done', data);

        if (data.result.error) {
          self.showError(container, data, data.result.error);
          return;
        }

        self.showSuccess(container, data);
        datas = self.getRest(datas, data.myindex, 'myindex');
        container.find('[data-index=' + data.ttindex + '] .content').css('backgroundImage', 'url(/' + data.result.path + ')');

        console.log('rest datas', datas);
      }
    }, options);

    // 初始化上传
    fileInput.fileupload(self.cfgs);

    // 删除文件
    container.on('click', '.glyphicon-trash', function() {
      let removed;
      const item = $(this).closest('[data-index]');
      const myindex = item.data('index');

      item.remove();
      datas = self.getRest(datas, myindex, 'myindex');
      removed = self.getRest(datas, myindex, 'myindex', {
        getRemoved: true
      });

      if (removed.length) {
        removed[0].abort();
      }

      if (!datas.length) {
        self.disableBtn(uploadBtn, '开始上传');
      }
    });

    // 开始上传
    uploadBtn.on('click', () => {
      datas.forEach((data) => {
        data.submit();
      });
    });
  },

  enableBtn(btn, text) {
    btn.prop('disabled', false).removeClass('disabled');
    if (text) btn.html(text);
  },

  disableBtn(btn, text) {
    btn.prop('disabled', true).addClass('disabled');
    if (text) btn.html(text);
  },

  showError(container, data, text) {
    const item = container.find('[data-index=' + data.myindex + ']');

    if (text) {
      item.find('.error .msg').html(text);
    } else if (data.errorThrown) {
      item.find('.error .msg').html(data.errorThrown);
    }

    item.find('.error').show();
    item.find('.tt-progress span').hide().css('width', 0);
  },

  showSuccess(container, data) {
    const item = container.find('[data-index=' + data.myindex + ']');

    item.data('completed', true).find('.done').show();
    item.find('.tt-progress span').hide().css('width', 0);
  },

  getRest(arr, value, prop, {
    getRemoved
  } = {}) {
    let rest = arr.slice();
    let removed = [];

    for (let i = 0; i < rest.length; i++) {
      if (prop && rest[i][prop] === value || !prop && rest[i] === value) {
        removed = rest.splice(i, 1);
        break;
      }
    }

    if (getRemoved) {
      return removed;
    }

    return rest;
  }
};
```

see more: [jQuery-File-Upload](https://github.com/blueimp/jQuery-File-Upload)
