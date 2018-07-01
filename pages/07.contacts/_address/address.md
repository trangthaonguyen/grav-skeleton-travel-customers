---
title: Our Address

map: '<iframe src="https://maps.google.com/maps?f=q&amp;source=s_q&amp;hl=en&amp;geocode=&amp;q=Glasgow,&amp;aq=&amp;sll=46.975033,31.994583&amp;sspn=0.368248,0.617294&amp;vpsrc=6&amp;ie=UTF8&amp;hq=&amp;hnear=Glasgow,+Glasgow+City,+United+Kingdom&amp;t=m&amp;ll=55.866932,-4.256344&amp;spn=0.020324,0.070896&amp;z=13&amp;output=embed"></iframe>'

address: 
  title: Travel Guide
  info: '8901 Marmora Road,<br>Glasgow, D04 89GR.<br>Telephone: +1 800 123 1234<br>E-mail: <a href="#">mail@bteamny.com</a>'

form_title: Contact Form


testimonials: 
  headline: Testimonials
  items: 
    - 
      name: Alex Williams
      url: '#'
      label: http://demolink.org
      content: Lorem ipsum dolor sit amet conse ctetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna. Ipsum dolor sit amet conse ctetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua
    - 
      name: Jesica Smith
      url: '#'
      label: http://demolink.org
      content: Lorem ipsum dolor sit amet conse ctetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna. Ipsum dolor sit amet conse ctetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua


form:
    name: ajax-contact-form
    classes: form-horizontal
    action: '/contacts'
    template: form-messages
    refresh_prevention: true

    fields:
        - name: name
          label: Your full name
          show_label: false
          placeholder: Your full name
          autocomplete: on
          type: text
          outerclasses: span3 control-group
          labelclasses: control-label
          wrapper_classes: controls
          classes: span3
          validate:
            required: true

        - name: email
          label: Your email
          show_label: false
          placeholder: Your email
          type: email
          outerclasses: span3 control-group
          labelclasses: control-label
          wrapper_classes: controls
          classes: span3
          validate:
            required: true

        - name: phone
          label: Phone number
          show_label: false
          placeholder: Phone number
          autocomplete: on
          type: text
          outerclasses: span3 control-group
          labelclasses: control-label
          wrapper_classes: controls
          classes: span3
          validate:
            required: true

        - name: message
          label: Message
          show_label: false
          placeholder: Message
          type: textarea
          outerclasses: span9 control-group
          labelclasses: control-label
          wrapper_classes: controls
          classes: span9
          validate:
            required: true

        - name: g-recaptcha-response
          label: Captcha
          show_label: false
          type: captcha
          outerclasses: span9 control-group capthca
          labelclasses: control-label
          wrapper_classes: controls
          recaptcha_site_key: RECAPTCHA_SITE_KEY
          recaptcha_not_validated: 'Captcha not valid!'
          validate:
            required: true

    buttons:
        - type: submit
          value: Submit
          classes: submit

    process:
        - captcha:
            recaptcha_secret: RECAPTCHA_SECRET
        - email:
            from: '{{ config.plugins.email.from }}'
            to: ['{{ config.plugins.email.to }}', '{{ form.value.email }}']
            subject: '[Site Contact Form] {{ form.value.name|e }}'
            body: '{% include ''forms/data.html.twig'' %}'
        - save:
            fileprefix: contact-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Thank you for getting in touch!
---