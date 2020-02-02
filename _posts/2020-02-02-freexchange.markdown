---
layout: post
title:      "FreExchange"
date:       2020-02-02 18:13:30 +0000
permalink:  freexchange
---


This is an app that will allow users to exchange items for events (like holloween) at will. It's pretty simple, you enter what you want, what you are willing to offer to other, wait for someone to is interested, and meet up!

When creating the rails api I made sure to add the api flag `--api` to avoid the creation of unnecessary files. Another important bit for the front end and back end to communicate was installing the cors gem, as well as uncommenting the cors.rb file. To meet the MVP I started out by creating 2 out of the 3 *essential* models, posts and comments. I also made corresponding database tables, and controllers. Each controller contains DRY CRUD actions. Each action in the posts controller includes comments, allowing me to submit one get request for both models. 
```
render json: @post,include:[:comments],status: 200
```

The file structure for the front end was manually done and it consists of three directories (imgs, src, and styles) and the index.html file. The "src" dir is what hold all the functionality. In there I have two sub directories (adapter and components). The adapter's sole purpose is to connect the rails api to the front end of the application. It is composed of a constructure that holds the base URL and a getPosts method resposinble for the GET request to the api. 
```
return fetch(`${this.baseUrl}/posts`).then(res => res.json())
```
It also contains two methods responsible for making POST requests to the rails apiafter form submissions.
In my components sub directory I have a posts.js file responsible for the bulk of my functionality. It creates all event listeners, fetching and posting comments and posts, creating and posting comments and posts, and also creating the comments form.
```
createCommentForm(ele) {
        const form = document.createElement("form")
        const textBox = document.createElement("input")
        const submit = document.createElement("button")
        
        submit.textContent = "Submit comment"
        submit.classList.add("btn", "btn-primary", "comment-submit")
        
        textBox.name = "commentContent"
        textBox.setAttribute("type", "text")
        textBox.placeholder = `Enter a comment:`
        textBox.classList.add("form-control", "comment-input")
        
        form.setAttribute("data-id", ele.dataset.id)
        
        form.append(textBox, submit)
        ele.parentElement.appendChild(form) 
        form.addEventListener('submit', (e) => {
            e.preventDefault()
            
            this.postComment(e)
        })
    }
```
My post.js file in this sub directory is responsible for rendering each post and comment (comments are rendered through a comment button) to the browser.
```
renderLi() {
        return `
            <div class="text-center">
                    <div class="container mb-1" data-id="${this.id}">
                        <div class="text-monospace">
                            <h4>What I Want:</h4> ${this.item1}
                        </div>
                        <div class="text-monospace">
                            <h4>What I'm Offering:</h4> ${this.item2}
                        </div>
                            <div class="interactive-comments post-${this.id} text-monospace"> 
                            <button class="create cmt-btn" data-id=${this.id} id="commentBtn">Comment: </button>
                        </div>
                    </div>
            </div>
            `
    }
}
```
I use the bootstrap framework on this project, I used the bootstrap CDN which made it simple to add and use. All css is in my styles subdirectory. I was easily able to add images to the site:
```
.container {
    list-style-position:inside;
    /* border: 1px solid black; */
    color: white;
    /* background-color:rgb(255, 153, 153); */
    background-image: url('../images/wood.jpg');
    background-repeat: no-repeat;
    background-size: 2000px 300px;
    padding-bottom: 2rem;
}
```

I truly feel great about this idea, and hope to develope this into a more functional application.
