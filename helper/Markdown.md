***# **Markdown**

| [Official Site ](https://daringfireball.net/projects/markdown/) | [Official Doc](https://daringfireball.net/projects/markdown/syntax) |
| :---: | :---: |

![](../logos/Markdown-v1-128x128.png)

### Styles

```markdown
# H1
## H2
### H3
#### H4
##### H5
###### H6
```
# H1
## H2
### H3
#### H4
##### H5
###### H6

```markdown
**bold**
*italic*
`code`
~~rayer~~
```
**bold**
*italic*
`code`
~~rayer~~


### Table
```markdown
| table | are | simple |
| :--- | :---: | ---: |
| when you | used | to |
| left| center | right |
```
| table | are | simple |
| :--- | :---: | ---: |
| when you | used | to |
| left| center | right |


### Links
```markdown
[Official Doc](https://daringfireball.net/projects/markdown/syntax)
[Relative Link](../helper/Common.md)
```
[Official Doc](https://daringfireball.net/projects/markdown/syntax)
[Relative Link](../helper/Common.md)


### Images
Inline:
```markdown
![alt text](../logos/Markdown-v1-128x128.png "Logo Title Text 1")
![alt text](../logos/Markdown-v1-128x128.png "Logo Title Text 1")
```
![alt text](../logos/Markdown-v1-128x128.png "Logo Title Text 1")

With Definition & Reference:
```markdown
[logo]: ../logos/Markdown-v1-128x128.png "Logo Title Text 2"
![alt text][logo]
```
[logo]: ../logos/Markdown-v1-128x128.png "Logo Title Text 2"
![alt text][logo]


### Highlight syntax
```markdown
    ```php
     $str = "hello World";
     $int = 0;
     $array = array();
    ```
```
```php
 $str = "hello World";
 $int = 0;
 $array = array();
```

### Blockquotes
```Markdown
 > Blockquotes are simple
 > and this line is a part of this simple.
```
> Blockquotes are simple
> and this line is a part of this simple.
