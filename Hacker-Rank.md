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
