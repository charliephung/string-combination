# string-combination

```javascript
const stringCombination = str => {
  let dict = [];
  const replace = (str, p, i = 0) => {
    if (i >= p.length) return;
    const newStr = str.replace(p[i], String.fromCharCode(96 + Number(p[i])));
    dict.push(transform(newStr));
    if (str.includes(p)) {
      replace(str, p, i);
    } else {
      i += 1;
      replace(str, p, i);
    }
    if (newStr.includes(p)) {
      replace(newStr, p, i);
    } else {
      i += 1;
      replace(newStr, p, i);
    }
  };

  replace(str, findComp(str));
  dict.push(transform(str));
  return dict;
};

const findComp = str => {
  let result = [];
  for (let i = 0; i < str.length - 1; i++) {
    if (Number(str[i] + str[i + 1]) < 26) {
      result.push(str[i] + str[i + 1]);
    }
  }
  return result;
};

const transform = str => {
  return str
    .split("")
    .map(c => (!isNaN(c) ? String.fromCharCode(96 + Number(c)) : c))
    .join("");
};

console.log(stringCombination("12258"));
// [ 'lbeh', 'aveh', 'abyh', 'lyh', 'abbeh' ]
```
