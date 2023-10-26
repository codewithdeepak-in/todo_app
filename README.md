# Todo Application.

<pre>
  import { useEffect, useState } from "react";
import "../src/style.css";

const App = () => {
  const [task, setTask] = useState("");
  const [addTask, setAddTask] = useState([]);
  const [mark, setMark] = useState([]);

  useEffect(() => {
    const data = JSON.parse(localStorage.getItem("tasks"));
    const mark = JSON.parse(localStorage.getItem("mark"));
    if (data && data.length > 0) {
      setAddTask(data);
    }
    if (mark && mark.length > 0) {
      setMark(mark);
    }
  }, []);

  useEffect(() => {
    localStorage.setItem("tasks", JSON.stringify(addTask));
    localStorage.setItem("mark", JSON.stringify(mark));
  }, [addTask, mark]);

  function handleSubmit(e) {
    e.preventDefault();
    if (task.length === 0) {
      alert("Please enter a task");
    } else {
      setAddTask([...addTask, task]);
      setTask("");
    }
  }

  function handleDelete(index) {
    const newArray = addTask.filter((item, ind) => ind !== index);
    setAddTask(newArray);
    setMark(mark.filter((item) => item !== index));
  }

  function handleMark(index) {
    if (!mark.includes(index)) {
      setMark([...mark, index]);
    } else {
      setMark(mark.filter((item) => item !== index));
    }
  }

  return (
    <div className="container">
      <div className="main_container">
        <div className="main_section">
          <div className="heading">Create Your To-Do List.</div>
          <br />
          <div>
            <form onSubmit={handleSubmit}>
              <input
                type="text"
                placeholder="Add New Task"
                onChange={(e) => setTask(e.target.value)}
                value={task}
              />
              <button>Add</button>
            </form>
          </div>
          <div className="todolist">
            {addTask.map((item, index) => (
              <div className="todoitem">
                <div
                  key={index}
                  className={mark.includes(index) ? "active" : ""}
                >
                  {item}
                </div>
                <div className="buttons">
                  <button onClick={() => handleMark(index)}>✔️</button>
                  <button onClick={() => handleDelete(index)}>❌</button>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  );
};

export default App;

</pre>
