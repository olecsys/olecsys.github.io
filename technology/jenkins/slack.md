Понадобилось мне реализовать отсылку прямых сообщений в [Slack](https://www.slack.com). Для взаимодействия с [Slack](https://www.slack.com) в [Jenkins](https://www.jenkins.io) есть плагин [slack-plugin](https://github.com/jenkinsci/slack-plugin).
В итоге выяснилось, что прямые сообщения пользователям можно посылать не по `user id` slack, а по первой части электронной почты. Т.е. если у вас есть пользователь с `user id` slack `test` почтой `email@emaildomain.org`, то послать в `Jenkins Pipeline` можно так:
```

```
В общем, как-то так.