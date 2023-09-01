# class-assignment-12-notesWall

## hosted link :- https://rohitdhawale07.github.io/class-assignment-12-notesWall/

This is project of crating a notes Wall.
In input box when u type something and clicking on add note button or keyboard enter button notes get printed below the box.
Firsly we created a HTML content using input box, button for add note and color type and below div printing for notes we added.
## HTML code
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NotesWall</title>
    <link rel="stylesheet" href="./style.css">
    <script defer src="./index.js"></script>
</head>
<body>
    
<div class="header">
    <div class="content">
        <div class="note-input">
            <textarea name="" id="" cols="30" rows="3" class="input-text get-note" placeholder="// Write a note here"></textarea>
            <div class="action">
                <input type="color" name="" id="" value="#ccffcc" class="theme get-color">
                <button id="add-btn">Add note</button>
            </div>
        </div>
    </div>
</div>

<div class="notes-list">
    <div class="no-notes">
        <h4 class="msg">You haven't added notes yet.</h4>
    </div>
</div>

</body>
</html>
```
Then we create a Styling part for html content as below
## CSS code
```
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
.header{
    background-color: rgb(245, 245, 245);
}
.content{
    max-width: 800px;
    margin: auto;
    padding: 20px;
}
.note-input{
    margin-top: 30px;
    padding: 20px;
    display: flex;
    flex-direction: row;
}
.input-text{
    height: 120px;
    width: 550px;
    padding: 10px;
    box-shadow: 5px 5px #586781;
    background-color: #ffffff;
    border-radius: 8px;
    font-size: 18px;
}
.action{
    display: flex;
    flex-direction: column;
    margin: 1rem;
}
.theme{
    width: 100px;
    height: 40px;
    cursor: pointer;
    color: yello;
}
#add-btn{
    background-color: aquamarine;
    color: black;
    box-shadow: 5px 5px #586781;
    margin: 0.50rem 0rem;
    width: 100px;
    height: 40px;
    font-size: 18px;
    font-weight: 500;
    cursor: pointer;
}
#add-btn:hover{
    scale: 1.01;
    border: 4px solid rgb(219, 216, 216) ;
}
.notes-list{
    max-width: 1000px;
    align-items: center;
    justify-content: center;
    margin: auto;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    margin-top: 1rem;
}
.no-notes{
    display: flex;
    flex-direction: row;
}
.msg{
    margin-top: 100px;
    text-align: center;
    opacity: 70;
    font-weight: 600;
    margin-bottom: 15px;
    line-height: 1.2;
    font-size: 1.5rem;
}
```
Coming to JS part fisrtly we get all those id's by using querySelector() method.
Then we added Event listener to the whole document using document.addEventListener() method using keyPress event.
After pressing a enter key we added our input text to printing div.
 Then created a addNewNote function which will work only when we added something to the input box.
 and created alert if without input text add note button is pressed.
 we also created a function of delete a note for deleting a note.
 code for js part is below.
 ## Javascript Code
 ```
const input = document.querySelector('.get-note');
const addNoteBtn = document.querySelector('#add-btn');
addNoteBtn.addEventListener("click", addNewNote);
const allNotes = [];

const color = document.querySelector('.get-color');
const notesList = document.querySelector('.notes-list');

document.addEventListener('keypress', (event) => {
    if (event.keyCode === 13) {
        addNewNote();
    }
})

function addNewNote() {
    if (input.value) {
        let newNote = {
            note: input.value,
            noteColor: color.value

        };
        allNotes.push(newNote);
    }
    else {
        alert("A note can't be empty.");

    }
   


    input.value = "";
    
    displayNotes(allNotes);

    
   
}


function displayNotes(notes) {
    notesList.innerHTML = " ";
    notes.forEach(element => {
       let noteHTML= `
        <div class="note" style="background-color:${element.noteColor};">
            <div class="note-view">
                ${element.note}
            </div>
            <div>
                <a class="deleteBtn">Del</a>
            </div>
        </div>
        `;

        notesList.insertAdjacentHTML('afterbegin', noteHTML);
        
        const deleteBtn = document.querySelector('.deleteBtn');
        deleteBtn.addEventListener('click', e => { deleteNote(e,element);})


    });
}


function deleteNote(e,element) {
    let item = e.target.parentElement.parentElement.parentElement;
    item.parentNode.removeChild(item);
    allNotes.pop(element);
    
}
```

