HookServe
=========

HookServe is a small golang utility for receiving github webhooks. 

```go
server := hookserve.NewServer()
server.Port = 8888
server.Secret = "supersecretcode"
server.GoListenAndServe()

for {
	select {
	case event := <-server.Events:
		fmt.Println(event.Owner + " " + event.Repo + " " + event.Branch + " " + event.Commit)
	default:
		time.Sleep(100)
	}
}
```

It also comes with a command-line utility that lets you pass webhook push events to other commands

```sh
$ hookserve logger -t PushEvent #log github webhook push event to the system log (/var/log/message) via the logger command
```

Setting up webhooks on github is easy. Navigate to `https://github.com/<your-name>/<your-repo>/settings/hooks' and create a new webhook. 

![Configuring webhooks in github](https://i.imgur.com/u3ciUD7.png)
