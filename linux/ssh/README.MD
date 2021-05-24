```
ssh-keygen -t RSA -N mypassword -f ~/.ssh/andreitgighub
```
-t какой алгоритм шифрования использовать
-N ключ шифрования
-f в какой файл сохранить ключ

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/github_stand
```
