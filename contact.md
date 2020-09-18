---
layout: default
title: Contact
---
<h2>Contact</h2>
<form id="contact-form"
  action="https://formspree.io/mdqvjybx"
  method="POST"
>
  <label for="email-field">メールアドレス *</label>
  <input id="email-field" type="email" name="email" />
  <label for="message-field">メッセージ *</label>
  <textarea id="message-field" type="text" name="message"></textarea>
  <p id="status"></p>
  <button type="submit" id="submit-button">送信</button>
</form>

<!-- Place this script at the end of the body tag -->

<script>
  window.addEventListener("DOMContentLoaded", function() {

    // get the form elements defined in your form HTML above
    var form = document.getElementById("contact-form");
    var submitButton = document.getElementById("submit-button");
    var status = document.getElementById("status");

    // Success and Error functions for after the form is submitted
    function success() {
      form.reset();
      submitButton.style = "display: none ";
      status.innerHTML = "送信しました！ありがとうございます！";
    }

    function error() {
      status.innerHTML = "送信失敗しました";
    }

    // handle the form submission event
    form.addEventListener("submit", function(ev) {
      ev.preventDefault();
      var data = new FormData(form);
      var email = data.get('email');
      var message = data.get('message');

      if (!/^\S+@\S+$/.test(email)) {
        status.innerHTML = "正確なメールアドレスを入力してください";
        return;
      }

      if (message.length === 0) {
        status.innerHTML = "メッセージを入力してください";
        return;
      }
      ajax(form.method, form.action, data, success, error);
    });
  });

  // helper function for sending an AJAX request
  function ajax(method, url, data, success, error) {
    var xhr = new XMLHttpRequest();
    xhr.open(method, url);
    xhr.setRequestHeader("Accept", "application/json");
    xhr.onreadystatechange = function() {
      if (xhr.readyState !== XMLHttpRequest.DONE) return;
      if (xhr.status === 200) {
        success(xhr.response, xhr.responseType);
      } else {
        error(xhr.status, xhr.response, xhr.responseType);
      }
    };
    xhr.send(data);
  }
</script>