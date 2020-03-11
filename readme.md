Javascript:

1. Destructing assignment is a special syntax that allows us to "unpack" arrays or objects into a bunch of variables, since sometimes they are more convenient. Destructurization also works fine with complex functions that have many parameters, default values , and so on.
const options = {
  title: "Menu",
  width: 100,
  height: 200
};
const { title } = options;
alert(title); // Menu

2. The template on the left side can determine the correspondence between properties and variables.
If we want to assign a property to a variable with a different name, for example, options.width to enter the variable name w, then we can set it using a colon:
let options = {
  title: "Menu",
  width: 100,
  height: 200
};
let {width: w, height: h, title} = options;
// width -> w
// height -> h
// title -> title
alert(title);  // Menu
alert(w);      // 100
alert(h);      // 200

3. Arrow function expressions have a shorter syntax than function expressions and are lexically bound to the value of this (but are not bound to the proper this, arguments, super, or new.target).
Arrow function expressions do not allow you to specify a name, so arrow functions are anonymous if they are not assigned to anything.

4. When using ‘my Function Call(++foo)’, the myFunction Call function is executed with the argument foo+1. And when using ‘my Function Call(foo++)', the myFunction Call function is executed with the foo argument , and after the function is executed, foo+1 occurs.
function test(value) {
  console.log(value)
}
let x = 1
test(x++) // '1'
// x = 2
test(++x) // '3'
// z = 3

5. Classes in JavaScript are syntactic sugar over the prototype inheritance mechanism that exists in JavaScript. The class s yntax d oes n ot i ntroduce a  new o bject-oriented m odel, b ut p rovides a  s impler a nd more i ntuitive w ay to c reate o bjects a nd o rganize i nheritance. I n fact, c lasses a re" special f unctions", s o j ust a s y ou d efine f unctions( function e xpressions a nd f unction declarations ), you can define classes using: class declarations and class expressions.

CSS:

6. Descificity is the way browsers determine which CSS property values best match an element and therefore will be applied. Specificity is based on matching rules consisting of different types of CSS selectors.
Specificity is the weight given to a specific CSS rule . The weight of a rule is determined by the number of each type of selector in this rule. If several rules have the same specificity, the last CSS rule in order is applied to the element . Specificity matters only in that case if one element matches multiple rules. According to the CSS specification , a rule for the directly relevant element will always have a higher priority than rules inherited from an ancestor.

7. When a modifier is used when declaring a style !important, this ad gets the highest priority among all other ads. Although technically a modifier !important has nothing to do with specificity , it directly affects it. Because !important complicates debugging by disrupting the natural cascading of your styles, it is not welcome and should be avoided. If two mutually exclusive styles with a modifier are applied to an element !important, then a style with more specificity will be applied.
A few practical tips:

- Always try to use specificity as well !important use only in extreme cases
- Use it !important only in page styles that override site styles or external styles (library styles such as Bootstrap or normalize.css) 
- Never use !important if you are writing a plugin or mashup.
- Never use !important in the overall CSS of the site.

8. flex
Using flex, you can easily achieve the following requirements:

- Vertical alignment of the block inside the parent.
- Design all container children so that they distribute the available width/ height among themselves, regardless of how much width/ height is available.
- Make all columns in the layout the same height , even if the content in them is different.

9. There are times when negative margins can add nice little accents for design such as a slightly offset image or icon. But, if you are using a negative margin as an integral part of your page layouts, you might want to try and rework the code.
Instead of using a negative margin, maybe try floating an element? Or perhaps positioning it absolutely to its parent? Before you even consider a negative margin, please consider what would happen if other elements on the page changed height or width.

10. 

Unit tests:
11. 
12. 
13. 

React:

14. React test step1:
import React, { useState, useEffect, forwardRef } from 'react';
import styles from './App.module.css';

const App = forwardRef((props, ref) => {
  const [windowWidth, setWindowWidth] = useState(window.innerWidth);

  function handleWidthChange() {
    setWindowWidth(window.innerWidth);
  }
  useEffect(() => {
    window.addEventListener("resize", handleWidthChange);
  }, [])

  return (
    <div className="App">
      <div ref={ref} style={{ border: '1px solid' }}>
        <h3>Current window size:</h3>
        <span className={styles.windowWidthBox}>{`Current with is: ${windowWidth}`}</span>
      </div>
    </div>
  );
})
export default App;

15. React test step2:
import React, { useState, useEffect, useRef, forwardRef } from 'react';
import styles from './App.module.css';

const App = forwardRef((props, ref) => {
  const [windowWidth, setWindowWidth] = useState(window.innerWidth);
  const [height, setHeight] = useState('');

  function handleWidthChange() {
    setWindowWidth(window.innerWidth);
  }
  useEffect(() => {
    window.addEventListener("resize", handleWidthChange);
  }, [])
  function handleChange(e) {
    const height = +e.target.value;
    setHeight(height);
  }

  return (
    <div className="App">
      <div ref={ref} style={{ border: '1px solid', height }}>
        <h3>Current window size:</h3>
        <span className={styles.windowWidthBox}>{`Current with is: ${windowWidth}`}</span>
        <h3>Controll height of the block:</h3>
        <input type="number" onChange={handleChange} value={height} />
      </div>
    </div>
  );
})
export default App;

16. React test step3:
import React, { useState, useEffect, forwardRef } from 'react';
import styles from './App.module.css';
import widthHeightChange from './HeightHocComponent';

const App = forwardRef((props, ref) => {
  const [windowWidth, setWindowWidth] = useState(window.innerWidth);

  const { height, setHeight } = props;
  function handleWidthChange() {
    setWindowWidth(window.innerWidth);
  }
  useEffect(() => {
    window.addEventListener("resize", handleWidthChange);
  }, [])

  function handleChange(e) {
    const height = +e.target.value;
    setHeight(height);
  }

  return (
    <div className="App">
      <div ref={ref} style={{ border: '1px solid', height }}>
        <h3>Current window size:</h3>
        <span className={styles.windowWidthBox}>{`Current with is: ${windowWidth}`}</span>
        <h3>Controll height of the block:</h3>
        <input type="number" onChange={handleChange} value={height} />
      </div>
    </div>
  );
})
const AppComponent = widthHeightChange(App);
export default AppComponent;


HeightHocComponent.js
import React, { useState, useRef, useEffect } from 'react';
const widthHeightChange = (BaseComponent) => (props) => {
 
 const [height, setHeight] = useState('');
 const ref = useRef();
 useEffect(() => {
 const currentHeight = ref.current.offsetHeight;
 setHeight(currentHeight);
 }, [])
 return (
 <BaseComponent setHeight={setHeight} height={height} ref={ref}/>
 )
}
export default widthHeightChange;

RXjs:

17. Subject is a type of Observable object . The peculiarity of Subject is that It can send data simultaneously to a set of consumers, which can be registered already during the execution of Subject, while the execution of the standard Observable is performed uniquely for each of its calls.
Сhange the language of the page. After the user selects a language, we pass the value of the selected language to subject. After that, a subscription is triggered in which the language pack is loaded .
BehaviorSubject stores the last value it sent.
Data about the temperature outside. There is a page where you can place a variable number of components, and all of them need to know the temperature outside. As soon as we place a component on the page , it subscribes to BehaviorSubject, which is triggered when the temperature changes. As a result, it will get the last and subsequent temperature values.
ReplaySubject is able to store a specified number of recent values , which is set when the object is created.
Calculating the average of previously entered numbers . We have a ReplaySubject that stores the last , for example 3, values from which the average is calculated each time a new number is added.

18. this.array$ = of([1,2], [3,4], [5,6,7]);
    this.array$.pipe(
      concatMap(res => res)
    ).subscribe(res => console.log(res));

19. 
