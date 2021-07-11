---
layout: post
title:  "Useful links for react"
#date:   2019-03-23 21:03:36 +0530
categories: React
---



Let's begin with creating the react project app:

`npx create-react-app sample_app`

About react-grid-layout
[react-grid-layout](https://blog.logrocket.com/top-10-react-grid-components-and-libraries-for-2021/)

About graphs:
* [Graph options](https://www.tabnine.com/blog/top-11-react-chart-libraries/)
* [Rechart examples](https://www.freakyjolly.com/react-charts-examples/)


About passing data between components:
[Medium tutorial](https://nipunadilhara.medium.com/passing-data-between-different-components-using-react-c8e27319ee69)


About using axios:
[Amigos code](https://www.youtube.com/watch?v=i-hoSg8iRG0)

About deploying node and react together:
[Avan tutor](https://www.youtube.com/watch?v=xwovj4-eM3Y)

```javascript
/src
|__ /components
|   |__ Parent.js
|   |__ Child1.js
|   |__ Child2.js
|
|__ App.js 
```


```javascript
import React, { Component } from 'react';
import './App.css';
import Parent from './components/Parent';
class App extends Component {
  render() {
    return (
      <div className="App">
          <Parent/>
      </div>
    );
  }
}
export default App;
```

<p style="text-align: center">
    <img src="/assets/images/post2/Araguaney.jpeg"  alt="drawing" width="300"/>
</p>

 
