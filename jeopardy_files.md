# Jeopardy file/folder structure

## List of rounds in `rounds/`
Each round of jeopardy has its own folder under `rounds/`,
name of the round is the folder name.

## Round description in `round.json`
Each round has it's own description file under it's round folder.

```
{
  "name": "Rundenname",
  "double_jeopardy_count": 2,
  "points": [100, 200, 300, 400, 500],
  "categories": [
    {
      "name": "Test Group 1",
      "path": "cat_group_1",
      "answers": [
        {
          "type": "text",
          "data": "Hello World",
          "description": "Hello World is a common code to learn a new language.",
          "answer": "text describing the solution to the game master"
        }, ...
      ]
    }, ...
  ]
}
```

### Answer
* `text`
  * `data` is answer text.
* `img`, `audio`, `video`, `code`
  * `data` is filename in `path` of category.