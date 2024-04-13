

### Dynamically update DOM

```javascript
const newParagraph = document.createElement('p');
newParagraph.textContent = 'Another comment';
document.getElementById('root').append(newParagraph);
```