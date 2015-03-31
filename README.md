# Final Project Assignment 2: Explore One More! (FP2) 
DUE March 30, 2015 Monday (2015-03-30)

This is just like FP1, but where you do a different library. (Full description of FP1 is [on Piazza.][piazza])

During this assignment, you should start looking for teammates. See the project schedule [on Piazza.][schedule]

Write your report right in this file. Instructions are below. You can delete them if you like, or just leave them at the bottom.
You are allowed to change/delete anything in this file to make it into your report. It will be public.

This file is formatted with the [**markdown** language][markdown], so take a glance at how that works.

This file IS your report for the assignment, including code and your story.

Code is super easy in markdown, which you can easily do inline `(require net/url)` or do in whole blocks:
```
#lang web-server/insta
 
(struct post (title body))
 
(define BLOG
  (list (post "Third Post" "Wooow another post")
        (post "Second Post" "This is another post")
        (post "First Post" "This is my first post starting from the bottom up")))
 
(define (start request)
  (render-blog-page BLOG request))
 
(define (parse-post bindings)
  (post (extract-binding/single 'title bindings)
        (extract-binding/single 'body bindings)))


(define (render-blog-page a-blog request)
  (local [(define (response-generator embed/url)
            (response/xexpr
             `(html (head (title "My Blog project"))
                    (body
                     (h1 "My Blog project")
                     ,(render-posts a-blog)
                     (form ((action
                             ,(embed/url insert-post-handler)))
                           (input ((name "title")))
                           (input ((name "body")))
                           (input ((type "submit"))))))))
 
          (define (insert-post-handler request)
            (render-blog-page
             (cons (parse-post (request-bindings request))
                   a-blog)
             request))]
 
    (send/suspend/dispatch response-generator)))
 
(define (render-post a-post)
  `(div ((class "post"))
        ,(post-title a-post)
        (p ,(post-body a-post))))
 
(define (render-posts a-blog)
  `(div ((class "posts"))
        ,@(map render-post a-blog)))
```

### My Library: (library name here)
Write what you did!
Remember that this report must include:
 
* **a narrative of what you did**
  * Looked into more web based coding with scheme and I thought it was really interesting that there was a library and lang (which I still need to fully understand) that lets me produce a local machine web page (this reminds me of looking back at doing how-to tutorials of html).  I am enjoying seeing the actual making of a web page as I am following along with the documentation.  I wonder if I can write in everything together with the webserver based racket and this scheme coding in order to make a self-written blog server. I think that would be really cool, I do see alot of html in scheme and it's starting to pan out more and more on how it's really viable (to me anyway).  I've never actually seen scheme or heard of it before (before OPL) so it's just all new to me.  I tried to make adjustments to see what I can and can't do, and theres alot that goes into this, I'm not sure what libraries are used but I want to look into it further along with the web server.
  * I followed the code somewhat step by step, all hand typed. I then see what I can adjust to see how it actually works,  I liked how every step is just showing you how static a webpage can be, and how you can turn it into dynamic webpage building.  Which is pretty cool because blogging isn't just the person who writes it, it's the audience that also want to comment with their input,  it's very plain but I hope to jazz it up a bit when I learn more about how to write things very html-like.
* **the code that you wrote**
* **output from your code demonstrating what it produced**
* ![alt text](https://github.com/lqtran/FP2/blob/master/1.JPG "Output")
* **any diagrams or figures explaining your work** 
 
The narrative itself should be no longer than 350 words. Yes, you can add more files and link or refer to them. This is github, handling files is awesome and easy!

Ask questions publicly in the Piazza group.

### How to Do and Submit this assignment

1. To start, [**fork** this repository][forking].
1. Modify the README.md file and [**commit**][ref-commit] changes to complete your solution.
  2. (This assignment is just one README.md file, so you can edit it right in github without cloning)
  3. (You may need to clone and push if you want to add extra files)
1. [Create a **pull request**][pull-request] on the original repository to turn in the assignment.

<!-- Links -->
[piazza]: https://piazza.com/class/i55is8xqqwhmr?cid=411
[schedule]: https://piazza.com/class/i55is8xqqwhmr?cid=453
[markdown]: https://help.github.com/articles/markdown-basics/
[forking]: https://guides.github.com/activities/forking/
[ref-clone]: http://gitref.org/creating/#clone
[ref-commit]: http://gitref.org/basic/#commit
[ref-push]: http://gitref.org/remotes/#push
[pull-request]: https://help.github.com/articles/creating-a-pull-request

