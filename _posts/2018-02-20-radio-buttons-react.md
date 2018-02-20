---
title: "Create one radio button that acts like a checkbox using Reactjs"
tags: react radio-button fail
layout: post

---

This is a piece of knowledge, maybe not good knowledge but eeeeeeheheheeh...

Can someone make a simple short tutorial on how to create radio buttons using
React.js already ?

I really need to do everything in this world.

I will teach you how to create one, and only one radio button, that a user can
check and uncheck as he wish, and nothing more, no multiple radio buttons, no
form, no bullshit.

## You shouldn't do this, but I will teach you anyway

Why don't you use a checkbox, bruh ?

## Because I want it round, and I don't want to use CSS

First build a radio button class

```javascript
class RadioButton extends React.Component{
	constructor(props){
		super(props)
	}
	
	render(){
		<input type="radio" name="whatever" value="whatever" />
	}
}
```

Ok, easy. Now we want to have the ability to check our radio, so we add a nice
`checked` property :

```html
<input type="radio" name="whatever" value="whatever" checked={true|false} />
```

In HTML, `<input>` maintain their own state and update it based on user input.
In React mutable state is typically kept in the state property of components,
and only updated with `setState()`.

### This is the annoying step

Because, we really don't care about the user, and don't trust them. We will let
React control the state. This is why we talk about "controlled component".

So we add a new state, that we initialize in the constructor

```javascript
this.state = {
	checked: this.props.checked
}
```

Now we need to change the state when a user click on the button.
If you are a good boy, you should use the `onChange` property.

But if you are ~~retarded~~ average and have decided to use radio buttons
instead of checkboxes, you need to use `onClick` instead.

```html
<input type="radio" onClick={this.toggleCheck} name="whatever" value="whatever" checked={true|false} />
```

We now need to write a method that will do the job to check or uncheck the 
input by changing the state of our component :

```javascript
toggleCheck(e){
	this.setState((prevState, props) => ({
      checked: !prevState.checked
    }))
}
```

Oh, don't forget to bind `this` to the method in the constructor

```javascript
this.toggleCheck = this.toggleCheck.bind(this);
```

Is it done ? my god this is too long and too dumb

Final version

```javascript
class RadioButton extends React.Component {
  constructor(props){
    super(props)
    this.state = {
      checked: this.props.checked
    }
    this.toggleCheck = this.toggleCheck.bind(this);
  }
  toggleCheck(){
	this.setState((prevState, props) => ({
      checked: !prevState.checked
    }))
  }
  render(){
    return(
        <label>
          {this.props.name}
          <input type="radio" onClick={this.toggleCheck} value="whatever" name={this.props.name} checked={this.state.checked} />
        </label>
    )
  }
  
}

ReactDOM.render(
  <RadioButton name="Not a checkbox" checked={false} />,
  document.getElementById('root')
)
```

Bye loosers. Don't do this, it's dumb, I am dumb, I am sorry
