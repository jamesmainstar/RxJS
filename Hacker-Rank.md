### Lonely Integer
```javascript
const arr = [4, 9, 95, 93, 57, 4, 57, 93, 9]
const result = arr.reduce((a, b) => a ^ b)

console.log(result);
```
### Big Sorting
```javascript
arr.sort((a, b) => {
    const aLength = a.length;
    const bLength = b.length;

    if(aLength > bLength){
        return 1;
    }else if(aLength < bLength){
        return -1;
    }else{
        for(let i = 0; i < aLength; i++){
            let anum = Number(a[i]);
            let bnum = Number(b[i]);

            if(anum > bnum){
                return 1;
            }else if(anum < bnum){
                return -1;
            }
        }

        return 0;
    }
})
```
### Array Manipulation
#### Data
```javascript
/**
 * Hacker Rank
 * Array Manipulation
 */
const arrSize = 5;
const itemLength = 3;
const inputItem = [
    {
        startIndex: 1, endIndex: 2, score: 100
    },
    {
        startIndex: 2, endIndex: 5, score: 100
    },
    {
        startIndex: 3, endIndex: 4, score: 100
    }
];

let arr = [];

for(let i = 0; i < arrSize; i++){
    arr[i] = 0;
}
```

#### Solution
```javascript
for(let i = 0; i < itemLength; i++){
    const self = inputItem[i];
    for(let j = self.startIndex - 1; j < self.endIndex; j++){
        arr[j] += self.score;
    }
}

console.log(arr);
console.log(Math.max.apply(null, arr));
```

#### Best Solution
```javascript
//Score의 사용범위를 지정하여 루프와 연산 비용을 줄인다.

for(let i = 0; i < itemLength; i++){
    const self = inputItem[i];

    //Score가 사용될 index를 지정한다.
    arr[self.startIndex - 1] += self.score;

    //Score가 미사용될 index를 지정한다.
    if(self.endIndex < arrSize){
        arr[self.endIndex] -= self.score;
    }
}

let sum = 0;
let max = 0;

for(let i = 0; i < arrSize; i++){
    sum += arr[i];

    if(sum > max){
        max = sum;
    }
}

console.log(arr);
console.log(max);
```
