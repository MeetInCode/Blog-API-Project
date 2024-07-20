to run this 2 terminals
nodemon solution.js
nodemon server.js 
then localhost:4000

when i want to crate a new post the flow

 1. link to /new which makes makes a get request to /new 
  <a id="newPostBtn" href="/new">New Post</a> 

 2. /new will render the modify.ejs page   
    app.get("/new", (req, res) => {
    res.render("modify.ejs", { heading: "New Post", submit: "Create Post" });
    });

 3. when submit button clicked make post request to /api/posts
    else {%> 
        <form id="newPostForm" method="post" action="/api/posts"> //go to api/posts
          <input type="text" name="title" placeholder="Title" required>
          <textarea name="content" placeholder="Content" required rows="10"></textarea>
          <input type="text" name="author" placeholder="Author" required>
          <button class="full-width" type="submit">
            <%= submit %>
          </button>
        </form>
        <% } %>

 4. make new post and redirected to /
 
        app.post("/api/posts", async (req, res) => {
        try {
            const response = await axios.post(`${API_URL}/posts`, req.body);
            console.log(response.data);
            res.redirect("/");
        } catch (error) {
            res.status(500).json({ message: "Error creating post" });
        }
        });

5. / will render to main home page that is index.ejs

        app.get("/", async (req, res) => {
        try {
            const response = await axios.get(`${API_URL}/posts`);
            console.log(response);
            res.render("index.ejs", { posts: response.data });
        } catch (error) {
            res.status(500).json({ message: "Error fetching posts" });
        }
        });


   here's a demo - 
![ezgif-6-c28c1179dc](https://github.com/user-attachments/assets/9f36e21e-358f-4de1-9e80-7b0d088ce716)
