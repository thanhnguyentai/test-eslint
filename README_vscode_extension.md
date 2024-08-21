# USE ESLINT AND PRETTIER WITH VSCODE EXTENSIONS

After setting up for eslint.config.js and prettier.config.js, we can work with eslint and prettier smoothly.\
But we can upgrade it to the next level: Currently we can only use them by run commands, but with their extensions for IDEs, we can use them right while editing files and get the result immediately.

### Install extensions by command for VSCode

We can manually install extensions, but it will take time if we work in a team and every member has to repeat it.\
To make it more convenient, we can create a command and each member just needs to run it for installing all same extensions.
- List extensions in `.vscode/extensions` file:
```
esbenp.prettier-vscode
dbaeumer.vscode-eslint
```
- Run `cat .vscode/extensions | xargs -L 1 code --install-extension`\
`cat .vscode/extensions`: read all in .vscode/extensions file \
`| xargs -L 1 code --install-extension`: loop each line from input and run `code --install-extension` with the current line

### Config VSCode to use installed extensions
- Add .vscode/settings.json file
- Add configs that are necessary for the project
- VSCode will use this file for configuring settings for the current project