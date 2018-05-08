Outline
- setTimeout(cb, 0) !== 0ms 
- currently working on a program the randomizes the time it takes to complete.  It simulates a user's playthough by randomizing when certain actions (e.g. button click, data submission) occur. 
- Note: for the purpose of this discussion "instantaneous" or "instant" means code that can run immediately (e.g. was not placed on a queue by setTimeout or setInterval) 
- setTimeout and setInterval have a minimum delay
  - 4ms in browsers
  - 1ms in node
- Implications
  - setting delay of 0ms with not happen instantaneous 
- Examples
  - chrome examples
  - node examples
- Nice to have
  - charts
  
