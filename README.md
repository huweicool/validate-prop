
[中文文档](https://github.com/huweicool/validate-prop/blob/master/README-Chinese.md)

# validate-prop

Test whether the data passes validation.


## Install

Install with [npm](https://www.npmjs.com/package/validate-prop)

```sh
  npm install --save validate-prop
```


## Usage

```js
import Validate from 'validate-prop';
// or
// const Validate = require("validate-prop");
const config = {
    userName: {
        type: 'notEmpty',
        message: 'The user name cannot be empty',
    },
    passworld: {
        type: 'notEmpty',
        message: 'The passworld cannot be empty',
    },
    phone: {
        message: "Incorrect phone number format",
        test: (value, key, rule) => {
            if (!value) {
                return "The cell phone number cannot be empty";
            }
            const isPhone = /^1[3456789]\d{9}$/.test(value);
            if (isPhone) {
                return null;
            } else {
                return "Incorrect phone number format";
            }
        },
    },
    code: [{
        type: "notEmpty",
        message: "The captcha cannot be empty",
    },{
        type: "length",
        value: [4, 6],
        message: "The captcha length is between 4 and 6",
    }],
};

const model = {
    userName: 'lucas',
    passworld: 'password123456',
    phone: "13912345678",
    code: "1234",
}
 Validate(config).start(model).then(({ error, key, result }) => {
    if( error ){
        // verification failed
        console.log(error); // error message
        return;
    }
    // verify successfully, do something
});
```

## Test
More examples to see the test
```sh
  npm test
```