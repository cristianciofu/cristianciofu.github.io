---
layout: post
title: Responsive Newsletters
---

The newsletters are an important part of any business. There's almost no website that doesn't send newsletters to its users.

> But, can these newsletters be... responsive? 

That's one question asked by a lot of people recently.


In the past 2 weeks I've been searching different solutions and/or ways that will allow me to do this - to do a **responsive newsletter**. One that will really be responsive. 

Unfortunately the result was not a very good one. I've found some solutions and some tricks, but for now the "perfect solution" is not here yet. And that's because each app / mail client / web app see things in its own way.

Anyway it depends a lot on what are you trying to make. There are ideas that you can really transform into **responsive newsletters** and idea that will not work. Simply as that. So it depends a lot on what are you trying to do :)

> What are you talking about? I'll use media queries and my job is done in 10 minutes!!!

No you won't. It's not that simple unfortunately... 

Most email clients are stripping the media queries, so all that hard work you've put in defining the breakpoints and sizing your elements it's actually completely ignored.

Here's a list with email clients that doesn't support **media query** ([from this article](https://litmus.com/blog/understanding-media-queries-in-html-email#support))

- Gmail app (iOS + Android)
- Inbox by Gmail app (iOS + Android)
- Android Outlook Exchange via native client
- Android Yahoo! Mail app
- Gmail (Android Browser)
- Mailbox (iOS + Android)
- Outlook.com (Android Browser)
- Yahoo! Mail (Android Browser)
- Windows Phone 7
- Windows Phone 8

Ok, enough talking, let me show you what I've found hoping that it will help you more that it helped me. 

### Email Client CSS / Media Queries Support

To see more details about the support of CSS properties / Media Queries, here are some links that list who supports what :

- http://templates.mailchimp.com/resources/email-client-css-support/
- https://www.campaignmonitor.com/css/
- https://litmus.com/help/email-clients/media-query-support/

### Responsive Newsletters Solutions 

There are few tools out there that are claiming they can help you build a good looking **responsive newsletter**.

- [Foundation for Emails](http://foundation.zurb.com/emails)
    - it's not bad, but has no support for the Gmail / Inbox apps
- [Email Framework](http://emailframe.work/)
    - the documentation is pretty straight forward but as **Foundation for Emails** it doesn't work in the Gmail / Inbox apps
- [antwort](https://github.com/InterNations/antwort)
    - antwort is not really a framework, it's mostly an example, but it *(kind of)* supports Gmail. I've tested it and it's not bad.
- [mjml](https://mjml.io)
    - on their website it says : "MJML is a markup language designed to reduce the pain of coding a responsive email". It's true, the language allows you to quickly build your newsletter, but I think that for more complex newsletters it may become difficult to do things exactly as you want it

Few days ago I found in [an article](https://www.smashingmagazine.com/2016/02/web-dev-reading-list-125/) posted in **Smashing Magazine** a [solution made entirely in CSS](https://medium.freecodecamp.com/the-fab-four-technique-to-create-responsive-emails-without-media-queries-baf11fdfa848#.f7gorqxkr). I didn't test this yet, but from the screenshots looks promising.


### CSS Inliner Tools

That's really a **must do**. Why? Why inline styles? Well, popular email clients strip out the CSS that exists in the `<style>` tag.

So here are few solutions that will help you with that :

- http://templates.mailchimp.com/resources/inline-css/
- http://foundation.zurb.com/emails/inliner.html
- http://premailer.dialect.ca/

### How do you test it ?

##### Are you willing to pay ?

There's a paid solution that seems super cool. That's [Litmus](https://litmus.com/). Unfortunately, the free version only allows you to test in 3 clients.

##### If not... here's the free "alternative"

So, if you want something free, you can use [PutsMail](https://putsmail.com/). They allow you to send HTML email to 10 email addresses. 


### Some interesting links

If you want to go deeper into the subject, there are a lot of articles online. Here's just few links that I think they're pretty interesting : 

- http://tedgoas.github.io/Cerberus/
    - A few simple, but solid patterns for responsive HTML emails. Even in Outlook and Gmail.
- http://pages.litmus.com/RWDsummit
    - a pretty nice collection of articles
- http://www.alsacreations.com/tuto/lire/1533-un-e-mail-en-html-responsive-multi-clients.html
    - a french article that shows a pretty simple solution to quickly build a responsive email


### Final tips (here's some code finally)

#### You can force Microsoft to ignore parts of the code with:

```html
  <!--[!if gte mso 9]><!-->
  // This will be ignored by Outlook 2007
  <![endif]-->

  <!--[!if gte mso 15]><!-->
  // This will be ignored by Outlook 2013
  <![endif]-->

  <!--[if !mso]><!-->
  // This will be ignored by all Microsoft Outlook
  <!--<![endif]-->
```

Here you can find the [Outlook version numbers](http://templates.mailchimp.com/development/css/outlook-conditional-css)

#### Hiding content in Outlook : 

```html
  <!--[if !mso]><!-->
  <td>Show this content on all devices and clients, except Outlook</td>
  <!--<![endif]-->
```

#### Hiding content in Gmail : 

```css
width: 0; max-height: 0; overflow: hidden; float: left;
```

#### Hiding content in WebMobile / Outlook & Gmail : 

```html
  <style>
    @media only screen and (max-width: 480px) { 
      *[class~=hideonmobile] { display: none !important;}       
    }
  </style>

  <table>
    <tr>
      <td class="hideonmobile">Hide this content on mobile devices</td>
        <!--[if !mso]><!-->
        <td style="width: 0; max-height: 0; overflow: hidden; float: left;">
          This content won't show up on Outlook and Gmail (and some other more clients)
        </td>
        <!--<![endif]-->
    </tr>
  </table>
```



### Conclusion

As I've said in the beginning of this article. I think that everything depends on **what** are you trying to do. Want something fancy? It will be pretty hard to make it responsive. Want something simple text-based and 1-2 images? Without hiding/showing elements? It will be easier and you probably have in the end a result that's not bad at all...

I hope this article helped you at least a little bit...

If you know some other solution or an interesting article please leave a comment and I'll update the article. Thanks!



> Note : english is not my first language so I apologize if I've made errors ;)


