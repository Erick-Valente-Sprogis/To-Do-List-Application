<style>
 
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
}

.container {
    min-height: 100vh;
    background: linear-gradient(185deg, #8A1D26, #010001);
    padding: 10px;
}

.todo-app {
    max-width: 545px;
    background-color: #ffffff;
    margin: 100px auto;
    padding: 40px 30px 70px;
    border-radius: 15px;
}

.todo-app:hover {
    box-shadow: 1px 2px 2px 3px #010001;
}

.todo-app h2 {
    display: flex;
    align-items: center;
    margin-bottom: 30px;
}

.todo-app h2 img {
    width: 30px;
    margin-left: 10px;
}

.row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: #efe2e2;
    border-radius: 10px;
    padding-left: 20px;
    margin-bottom: 25px;
}

input {
    flex: 1;
    border: none;
    outline: none;
    background: transparent;
    padding: 10px;
    font-weight: 14px;
}

button {
    border: none;
    outline: none;
    padding: 16px 50px;
    color: #ffffff;
    font-size: 16px;
    cursor: pointer;
    background-color: #8A1D26;
    border-radius: 10px;
}

button:hover {
    background-color: #C82826;
}

ul li {
    list-style: none;
    font-size: 17px;
    padding: 12px 8px 12px 50px;
    user-select: none;
    cursor: pointer;
    position: relative;
}

ul li::before {
    content: '';
    position: absolute;
    height: 28px;
    width: 28px;
    border-radius: 50%;
    background-image: url(unchecked.png);
    background-size: cover;
    background-position: center;
    top: 8px;
    left: 16px;
}

ul li.checked {
    color: #555555;
    text-decoration: line-through;
}

ul li.checked::before {
    color: #666666;
    background-image: url(checked.png);
}

ul li span {
    position: absolute;
    right: 0;
    top: 5px;
    width: 40px;
    height: 40px;
    font-size: 22px;
    color: #010001;
    line-height: 40px;
    text-align: center;
    border-radius: 50%;
}

ul li span:hover {
    background-color: #e14b48;
}
 
</style>

<body>
    <div class="container">
        <div class="todo-app">
            <h2>To-Do List <img src="notes.png" /></h2>
            <div class="row">
                <input type="text" id="input-box" placeholder="Enter Your Text Here: ">
                <button onclick="addTask()">ADD</button>
            </div>
            <ul id="list-container">
                <!--- <li class="checked">Task 0</li>
                <li>Task 1</li> --->
            </ul>
        </div>
    </div>
 
  <script>
    const listContainer = document.getElementById("list-container");
const inputBox = document.getElementById("input-box");

function addTask() {
    if (inputBox.value === '') {
        alert("Enter Some Data");
    }else {
        let li = document.createElement("li");
        li.innerHTML = inputBox.value;
        listContainer.appendChild(li);
        let span = document.createElement("span");
        span.innerHTML = "\u00d7";
        li.appendChild(span);
    }
    inputBox.value = "";
    saveTask();
}

listContainer.addEventListener("click", function(e){
    if (e.target.tagName === "LI") {
        e.target.classList.toggle("checked");
        saveTask();
    }else if (e.target.tagName === "SPAN") {
        e.target.parentElement.remove();
        saveTask();
    }
});

function saveTask () {
    localStorage.setItem("data",listContainer.innerHTML);
};

function showTask () {
    listContainer.innerHTML = localStorage.getItem("data");
};

showTask();
  </script>
