---
layout: post
title:  "Use TinyMCE"
date:   2017-02-22
categories: ['web development']
tags: ['javascript']
---

```js
export default {
  init(options = {}) {
    this.cfgs = $.extend({
      selector: 'textarea',
      menubar: false,
      language: 'zh_CN',
      plugins: 'autosave',
      toolbar: 'alignleft aligncenter alignright myimage mysave',
      height: 360,
      autosave_ask_before_unload: false,
      autosave_retention: '1440m',
      content_css: '/assets/plugins/tinymce/content.css',
      statusbar: false,
      setup: (editor) => {
        this.setup(editor);
      }
    }, options);

    tinymce.init(this.cfgs);
  },

  setup(editor) {
    if (this.cfgs.toolbar.indexOf('myimage') !== -1) {
      this.initModal();
      editor.addButton('myimage', {
        title: '插入图片',
        icon: 'image',
        classes: 'widget btn upload-image',
        onclick() {
          $('#editor-image-modal').modal({
            backdrop: 'static'
          });
        }
      });
    }

    if (this.cfgs.toolbar.indexOf('mysave') !== -1) {
      editor.addButton('mysave', {
        title: '保存草稿',
        icon: 'fa fa-floppy-o',
        classes: 'widget btn save-draft',
        onclick() {
          if ($.trim($(tinymce.activeEditor.getContent()).text()) !== '') {
            editor.plugins.autosave.storeDraft();
            console.log('草稿已保存');
          }
        }
      });
    }
  },

  initModal() {
    const title = '插入图片';
    const accept = '.gif, .jpg, .jpeg, .png';
    const msg = '支持jpg、png和gif格式的图片，最大5MB';
    const tpl = `
            <div id="editor-image-modal" class="modal editor-modal center-container fade">
              <div class="modal-dialog">
                <div class="modal-content">
                  <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
                    <h4>${title}</h4>
                  </div>
                  <div class="modal-body">
                    <div class="btns">
                      <input name="file" type="file" accept="${accept}" multiple />
                      <button type="button" disabled class="btn btn-info btn-upload disabled">开始上传</button>
                    </div>
                    <div class="msg">${msg}</div>
                    <div class="template-upload"></div>
                  </div>
                  <div class="modal-footer">
                    <button type="button" class="btn btn-default" data-dismiss="modal">取消</button>
                    <button type="button" disabled class="btn btn-primary btn-confirm disabled">${title}</button>
                  </div>
                </div>
              </div>
            </div>
          `;

    $(tpl).appendTo('body');
  }
};
```

see more: [tinymce docs](https://www.tiny.cloud/docs/)
