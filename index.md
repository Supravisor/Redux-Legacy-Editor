
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous" />
<link rel="stylesheet" href="styles.css" />

<style>

h1 > a {
  font-family: Corbel;
  color: white;
}

.markdown-body h1 {
  border-bottom: none;
}

.markdown-body table td, .markdown-body table tr {
  border: none;
}

input:not([type:"button"]) {
  border-color: black;
}

</style>

<form name="editor">
  <table>
    <tbody>
      <tr>
        <td id="buttons">

<p><input type="button" class="btn btn-primary" value="create a reducer function" onclick="document.editor.textbox.value+='\nconst ' + document.editor.reducerName.value + ' = (state = ' + document.editor.state.value + ') => {\n  return state;\n}\n\n'" />
Name:  <input class="btn" value="reducer" name="reducerName" size="10" type="textfield" />
State: <input class="btn" value="initial" name="state" size="10" type="textfield" /></p>

<p><input type="button" class="button btn btn-primary" value="define store" onclick="document.editor.textbox.value+='const store = Redux.createStore(reducer);\n'" />
   <input type="button" class="btn btn-success" value="define store and create a reducer function" onclick="document.editor.textbox.value+='const store = Redux.createStore(\n  (state = ' + document.editor.reducerName.value + ') => state\n);\n\n'" /></p>

<p><input type="button" class="button btn btn-primary" value="get state from Redux store" onclick="document.editor.textbox.value+='const currentState = store.getState();\n'" /></p>

<hr />

<!-- define a Redux action -->

<p><input type="button" class="button btn btn-primary" value="define a Redux action I" onclick="document.editor.textbox.value+='\nconst ' + document.editor.action.value + ' = {\n  type: &#34;' + document.editor.actionType.value + '&#34;\n}\n'" />

  <input class="btn" value="action" name="action" size="10" type="textfield">
  <input class="btn" value="type" name="actionType" size="10" type="textfield"></p>
  
<p><input type="button" class="button btn btn-primary" value="define an action creator" onclick="document.editor.textbox.value+='\nfunction ' + document.editor.actionCreator.value + '() {\n  return ' + document.editor.action.value + ';\n}\n'" />

  <input class="btn" value="actionCreator" name="actionCreator" size="10" type="textfield"></p>

<p><input type="button" class="button btn btn-primary" value="define a Redux action II" onclick="document.editor.textbox.value+='\nconst ' + document.editor.actionCreator.value + ' = () => {\n  return {\r    type: &#34;' + document.editor.actionType.value + '&#34;\n  }\n};\n'" /></p>
  
<p><input type="button" class="button btn btn-primary" value="dispatch an action event indirectly" onclick="document.editor.textbox.value+=document.editor.data.value === '' ? '\nstore.dispatch(' + document.editor.actionCreator.value + '());\n' : '\nstore.dispatch(' + document.editor.actionCreator.value + '(&#34;' + document.editor.data.value + '&#34;));\n'" />
  <input class="btn" name="data" placeholder="data" size="10" type="textfield"></p>

<p><input type="button" class="button btn btn-success" value="dispatch an action event directly" onclick="document.editor.textbox.value+='\nstore.dispatch({ type: &#34;' + document.editor.actionType.value + '&#34; });\n'" />
</p>

<hr />

<p><input type="button" class="button btn btn-primary" value="defaultState" onclick="document.editor.textbox.value+='\nconst defaultState = {\n' + '  '+ defaultStateKey.value + ': ' + defaultStateValue.value + '\n};\n'">
 <input class="btn" value="key" name="defaultStateKey" size="10" type="textfield">
 <input class="btn" value="value" name="defaultStateValue" size="10" type="textfield"></p>

<!-- reducer functions -->

<p><input type="button" class="button btn btn-success" value="handle a single action" onclick="document.editor.textbox.value='\nconst defaultState = {\n  ' + document.editor.defaultStateKey.value + ': ' + document.editor.defaultStateValue.value + '\n};\n\nconst ' + document.editor.reducerArgument.value.replace(' ', '').toUpperCase() + ' = &#34;' + document.editor.reducerArgument.value.replace(' ', '').toUpperCase() + '&#34;;\n\nconst reducer = (state = defaultState, action) => {\n  if (action.type === ' + document.editor.reducerArgument.value.toUpperCase() + ') {\n    return {\n     ' + document.editor.defaultStateKey.value + ': ' + document.editor.reducerValue.value + '\n    };\n  } else {\n    return state;\n  }\n};\n\nconst store = Redux.createStore(reducer);\n\nconst ' + document.editor.reducerAction.value + ' = () => {\n  return {\n    type: '+ document.editor.reducerArgument.value.toUpperCase() + '\n  }\n};'"></p>

<p><input class="btn" value="action" name="reducerAction" size="10" type="textfield">
 <input class="btn" value="argument" name="reducerArgument" size="10" type="textfield">
 <input class="btn" value="value" name="reducerValue" size="10" type="textfield"></p>

<p><input type="button" class="button btn btn-primary" value="handle multiple actions" onclick="document.editor.textbox.value+='\nconst reducer = (state = defaultState, ' + document.editor.reducerAction.value + ') => {\n    switch (action.type) {'"></p>

<p><input type="button" class="button btn btn-primary" value="@ case" onclick="switchCase()">
 <input class="btn" value="action" name="caseAction" size="10" type="textfield">
 <input class="btn" value="value" name="caseValue" size="10" type="textfield"></p>

<p><input type="button" class="button btn btn-success" value="default" onclick="handleMultipleActions()"></p>

<hr />

<!-- subscribe listener function -->

<p><input type="button" class="button btn btn-primary" value="subscribe a listener function" onclick="document.editor.textbox.value+='\nstore.subscribe(() => {' + document.editor.storeListenerFunction.value + '});\n'">
  <input class="btn" value="function" name="storeListenerFunction" size="10" type="textfield"></p>

<hr />

<!-- handle multiple reducers -->

<p><input type="button" class="button btn btn-primary" value="handle multiple reducers" onclick="document.editor.textbox.value+='\nconst rootReducer = Redux.combineReducers({'"></p>

<p><input type="button" class="button btn btn-primary" value="@ reducer" onclick="document.editor.textbox.value+='\n  ' + document.editor.multipleReducerKey.value + ': ' + document.editor.multipleReducerValue.value + ','">

<input type="button" class="button btn btn-primary" value="last reducer" onclick="document.editor.textbox.value+='\n  ' + document.editor.multipleReducerKey.value + ': ' + document.editor.multipleReducerValue.value"></p>

<p><input class="btn" value="key" name="multipleReducerKey" size="10" type="textfield">
  <input class="btn" value="reducer" name="multipleReducerValue" size="10" type="textfield"></p>

<p><input type="button" class="button btn btn-success" value="close reducers" onclick="document.editor.textbox.value+='\n});\n\nconst store = Redux.createStore(rootReducer);\n'"></p>

<hr />

<!-- handle asynchronous actions -->

<p><input value="REQUEST" name="request" size="10" type="textfield"></p>

        </td>
        <td id="textbox">
          <textarea id="preview" name="textbox"></textarea>
        </td>
      </tr>
    </tbody>
  </table>
</form>

<script src="./script.js"></script>
