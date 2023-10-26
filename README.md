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
   // JSX
};

export default App;

</pre>
