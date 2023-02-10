# reusable
code to developed app for book library
<html>
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <style>
      table {
        width: 100%;
        border-collapse: collapse;
      }
      
      th, td {
        border: 1px solid black;
        padding: 8px;
        text-align: left;
      }
      
      th {
        background-color: #f2f2f2;
      }
      
      tr:nth-child(even){
        background-color: #f2f2f2;
      }
    </style>
    <script>
      function searchBooks() {
        var subject = $("#subject").val();
        var query = $("#query").val();
        var url = "https://openlibrary.org/search.json?subject=" + subject + "&q=" + query;

        $.get(url, function(data) {
          var books = data.docs;
          var bookList = "<table><tr><th>Book Name</th><th>Author Name</th><th>Publication Year</th></tr>";
          for (var i = 0; i < 10 && i < books.length; i++) {
            bookList += "<tr><td>" + books[i].title + "</td><td>" + books[i].author_name + "</td><td>" + books[i].first_publish_year + "</td></tr>";
          }
          bookList += "</table>";
          $("#bookList").html(bookList);
        });
      }
    </script>
  </head>
  <body>
    <h1>Books Library App</h1>
    <p>Select a subject:</p>
    <ul>
      <li><a href="#" onclick="searchBooks('Fiction')">Fiction</a></li>
      <li><a href="#" onclick="searchBooks('history')">History</a></li>
      <li><a href="#" onclick="searchBooks('science')">Science</a></li>
      <li><a href="#" onclick="searchBooks('technology')">Technology</a></li>
      <li><a href="#" onclick="searchBooks('biography')">Biography</a></li>
    </ul>
    <p>Enter book and search:</p>
    <input type="text" id="subject" placeholder="Subject">
    <input type="text" id="query" placeholder="Author name">
    <button onclick="searchBooks()">Search</button>
    <h2>Results:</h2>
    <div id="bookList"></div>
  </body>
    <!-- ... -->
    <div id="bookList"></div>
    <br>
    <button id="prev">Previous</button>
    <button id="next">Next</button>
  </body>
  <script>
    var books = [];
    var currentPage = 0;
    var resultsPerPage = 10;
  
    function searchBooks() {
      var subject = $("#subject").val();
      var query = $("#query").val();
      var url = "https://openlibrary.org/search.json?subject=" + subject + "&q=" + query;
  
      $.get(url, function(data) {
        books = data.docs;
        currentPage = 0;
        displayResults();
      });
    }
  
    function displayResults() {
      var startIndex = currentPage * resultsPerPage;
      var endIndex = startIndex + resultsPerPage;
      var displayedBooks = books.slice(startIndex, endIndex);
      var bookList = "<table><tr><th>Book Name</th><th>Author Name</th><th>Publication Year</th></tr>";
      for (var i = 0; i < displayedBooks.length; i++) {
        bookList += "<tr><td>" + displayedBooks[i].title + "</td><td>" + displayedBooks[i].author_name + "</td><td>" + displayedBooks[i].first_publish_year + "</td></tr>";
      }
      bookList += "</table>";
      $("#bookList").html(bookList);
    }
  
    $("#prev").click(function() {
      if (currentPage > 0) {
        currentPage--;
        displayResults();
      }
    });
  
    $("#next").click(function() {
      if (currentPage < Math.ceil(books.length / resultsPerPage) - 1) {
        currentPage++;
        displayResults();
      }
    });
  </script>
  
  
</html>

