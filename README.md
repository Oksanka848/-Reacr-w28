# React w28

*1. В чем разница между контролируемыми и неконтролируемыми компонентами?*

В контролируемом компоненте данные обрабатываются внутри компонента (и изменять их состояние можно внутри компонента).
А в неконролируемом обработка происходит напрямую в DOM (данные для каждого элемента ввода хранятся в DOM, а не в компоненте).

*2. Есть ли смысл использовать метод `shouldComponentUpdate()` в `PureComponent`?*

есть , т.к. этот метод позволяет увеличить производительность средних и крупных проектов.

*3. Будет ли перерисовываться данный компонент?*

```
 class PureComponent extends React.PureComponent {
      state = {
        item: {
    			count:0
    		},
      }
      handleClick= () =>  {
        const item = this.state.item;
        item.count = this.state.item.count ++ ;
        this.setState({item});
      }
      render() {
        return <h2>{this.state.item.count}</h2>
      }
    }

```
будет

*4. Что будет, если чекбоксу не передать свойство '`checked`'?*

чекбокс не будет работать, поле будет не активным

*5. В чем главное преимущество использования `PureComponent`?*

Будет вызывать рендер только если обнаружит изменения в state или props компонента.
Таким образом сокращается количество рендеров в приложении, что увеличивает его производительность.

*6. Что будет, если компоненту `input` передать метод `onChange`, но не передать `value`?*

react не поймет что именно ему нужно будет обработать методом onChange
А что будет, если компоненту `input` передать `value`, но не передать метод `onChange`?
форма не изменится, т.к. не задан метод изменения состояния

*7. Как сделать из обычного `select` список с несколькими выбранными значениями (мультиселект)?*

В атрибут value передать массив

*8. Напишите пример валидации текстового поля на React - чтобы оно было не пустым
```
class Editor extends React.Component {
  constructor(props) {
    super(props);
    this.state = { text: this.props.text };
  }
  onChange = (e) => {
    this.setState({ text: e.target.value });
  };
  render() {
    return <textarea onChange={this.onChange} value={this.state.text} />;
  }
}
```

*9. Приведите пример простейшей формы логина на сторонних компонентах
(Formic, Material или Bootstrap на ваш выбор)*
```
import React from "react";
import { Formik, Form, Field, ErrorMessage } from "formik";
export default function App() {
  return (
    <div className="App">
      <Formik
        initialValues={{ firstName: "", lastName: "" }}
        validate={values => {
          const errors = {};
          if (!values.firstName) {
            errors.firstName = "Required";
          }
          return errors;
        }}
        onSubmit={(values, { setSubmitting }) => {
          setTimeout(() => {
            alert(JSON.stringify(values, null, 2));
            setSubmitting(false);
          }, 400);
        }}
      >
        {({ isSubmitting }) => (
          <Form>
            <Field type="text" name="firstName" />
            <br />
            <ErrorMessage name="firstName" component="div" />
            <br />
            <Field type="text" name="lastName" />
            <br />
            <ErrorMessage name="lastName" component="div" />
            <br />
            <button type="submit" disabled={isSubmitting}>
              Submit
            </button>
          </Form>
        )}
      </Formik>
    </div>
  );}
```
