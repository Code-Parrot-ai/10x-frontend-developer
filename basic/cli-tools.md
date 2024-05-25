---
title: CLI Tools every Developer should know
subtitle: Explore some essential CLI tools to enhance your development experience and productivity as a developer.
slug: top-10-cli-tools
tags: cli, productivity, development, tools
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716595292517/EC158zIuz.webp?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

The command line interface (CLI) is an essential tool for developers, providing powerful functionality that can streamline workflows and enhance productivity. Knowing how to use CLI tools effectively can help you work more efficiently, automate repetitive tasks, and troubleshoot issues quickly. In this article, we'll explore a few CLI tools to enhance your development experience.

I've tried my best to include tools that support multiple operating systems (Linux, macOS, and Windows) and are widely used in the developer community. Let's dive in!

**Oh My Zsh**

Oh My Zsh is a popular open-source framework for managing your Zsh configuration. It comes with a vast collection of plugins and themes that can enhance your command line experience. Oh My Zsh provides features like auto-completion, syntax highlighting, and custom prompts, making it a valuable tool for developers who spend a lot of time in the terminal.

Here's how you can install Oh My Zsh on your system:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

or using wget:

```bash
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

You can find more information on the official Oh My Zsh GitHub repository: [Oh My Zsh GitHub Repository](https://github.com/ohmyzsh/ohmyzsh)

**Tmux**

Tmux is a terminal multiplexer that allows you to create and manage multiple terminal sessions within a single window. It provides features like split panes, session management, and window management, making it easier to work with multiple tasks simultaneously. Tmux is a powerful tool for developers who need to work with multiple terminals at the same time. Commands like tmux new -s session_name, tmux attach -t session_name, and tmux kill-session -t session_name help in managing terminal sessions effectively.

You can follow this guide to install Tmux on your system: [Tmux Installation Guide](https://github.com/tmux/tmux/wiki/Installing)

**The F\*\*k**

The F**k (often referred to as "The F") is an incredibly useful tool for developers who often make typos or incorrect commands in the terminal. It automatically corrects errors in previous console commands, saving you time and frustration. By simply typing `fuck` after an incorrect command, The F suggests the correct command and runs it for you. This tool is especially useful for developers who work quickly in the terminal and occasionally mistype commands.

Here is the official installation guide for The fuck: [The fuck installation guide](https://github.com/nvbn/thefuck?tab=readme-ov-file#installation)

**Jq**

Jq is a lightweight and flexible command-line JSON processor that allows you to parse, filter, and manipulate JSON data effectively. It provides a set of powerful tools for working with JSON data, including querying, formatting, and transforming JSON objects. Jq supports features like filters, expressions, and functions that can help you work with complex JSON structures easily. Some essential Jq commands include `jq .`, `jq '.key'`, `jq '.key | select(.subkey == "value")'`, and `jq '.key | map(.subkey)'`. Learning how to use Jq can help you work with JSON data more efficiently and automate tasks that involve JSON processing.

You can install Jq using your package manager:

```bash
sudo apt-get install jq
```

or, if you're using macOS:

```bash
brew install jq
```

or, you can follow the installation instructions on the official Jq website: [Jq Installation Guide](https://stedolan.github.io/jq/download/)

**Bat**

Bat is a modern and feature-rich replacement for the `cat` command that provides syntax highlighting and line numbering for file contents. It allows you to view and read files with improved readability and aesthetics. Bat supports features like syntax highlighting for various file types, automatic paging, and Git integration, making it a valuable tool for developers who frequently work with text files. Some essential Bat commands include `bat`, `bat --line-range`, `bat --theme`, and `bat --language`. Learning how to use Bat can help you read and navigate files more effectively in the terminal.

You can install Bat using your package manager:

```bash
sudo apt-get install bat
```

or, if you're using macOS:

```bash
brew install bat
```

or, you can follow the installation instructions on the official Bat GitHub repository: [Bat Installation Guide](https://github.com/sharkdp/bat?tab=readme-ov-file#installation)

**Zoxide**

Zoxide is a fast directory navigation tool that helps you jump to your most frequently used directories with ease. It tracks the directories you visit and provides fuzzy matching to quickly navigate to them using the `z` command. Zoxide is a handy tool for developers who work with multiple projects and need to switch between directories frequently. It's lightweight, easy to use, and can significantly improve your productivity when working in the terminal. Some common Zoxide commands include `z`, `z -l`, `z -c`, and `z -r`.

You can follow the installation instructions for Zoxide on the official GitHub repository: [Zoxide Installation Guide](https://github.com/ajeetdsouza/zoxide?tab=readme-ov-file#installation)

**Ngrok**

Ngrok is a powerful tool that allows you to expose local servers to the internet securely. It creates secure tunnels to your localhost, making it easy to share web applications, APIs, and other services with collaborators or clients. Ngrok provides a set of command-line tools that allow you to start tunnels, inspect traffic, and manage your connections effectively. Some essential Ngrok commands include `ngrok http`, `ngrok tcp`, `ngrok status`, and `ngrok kill`. Learning how to use Ngrok can help you test webhooks, share projects in development, and collaborate with others seamlessly.

You can follow the official Ngrok installation guide for your operating system: [Ngrok Installation Guide](https://ngrok.com/download)

**Tldr**

Tldr (Too Long; Didn't Read) is a simplified and community-driven tool for viewing concise and practical examples of command-line commands. It provides quick reference guides for common commands, making it easier to understand their usage and options. Tldr is a valuable resource for developers who want to learn new commands, refresh their memory, or find examples of command-line tools. Some essential Tldr commands include `tldr`, `tldr --update`, `tldr --list`, and `tldr <command>`.

You can install Tldr using NPM:

```bash
npm install -g tldr
```

**HTTPie**

HTTPie is a user-friendly command-line HTTP client that makes it easy to interact with APIs and web services. It provides a simple and intuitive interface for sending HTTP requests, inspecting responses, and debugging network communication. HTTPie supports features like syntax highlighting, JSON output, and form data handling, making it a powerful tool for developers working with APIs. Some essential HTTPie commands include `http`, `http GET`, `http POST`, and `http PUT`. Learning how to use HTTPie can help you test APIs, debug network issues, and interact with web services more effectively. It can be used as an alternative to tools like cURL or Postman.

You can follow the installation instructions for HTTPie on the official GitHub repository: [HTTPie Installation Guide](https://httpie.io/cli)

**Fzf**

Fzf is a command-line fuzzy finder that helps you search and navigate through files, directories, and command history with ease. It provides interactive search capabilities with fuzzy matching, making it easy to find and open files quickly. Fzf integrates seamlessly with various command-line tools and can significantly improve your productivity when working in the terminal. Some common Fzf commands include `fzf`, `fzf --preview`, `fzf --preview "cat {}"`, and `fzf --reverse`.

You can install Fzf using git:

```bash
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

or, you can directly visit the official GitHub repository for more installation options: [Fzf Installation Guide](https://github.com/junegunn/fzf?tab=readme-ov-file#installation)

**Ffmpeg**

FFmpeg is a powerful multimedia framework that can decode, encode, transcode, mux, demux, stream, filter, and play almost anything that humans and machines have created. It supports a wide range of audio and video formats, making it a versatile tool for multimedia processing. FFmpeg provides a set of command-line tools that allow you to manipulate multimedia files, convert formats, extract streams, and perform various multimedia operations. Some essential FFmpeg commands include `ffmpeg -i input.mp4 output.mp4`, `ffmpeg -i input.mp4 -vn -acodec copy output.mp3`, and `ffmpeg -i input.mp4 -vf "scale=640:480" output.mp4`. Learning how to use FFmpeg can help you work with multimedia files, create custom video processing pipelines, and automate multimedia tasks effectively.

You can follow the official FFmpeg installation guide for your operating system: [FFmpeg Installation Guide](https://ffmpeg.org/download.html)

**Cobra**

Cobra is a modern and powerful CLI library for Go that makes it easy to create powerful and efficient command-line applications. It provides a simple and elegant API for building CLI tools with features like command routing, argument parsing, flag handling, and help generation. Cobra is widely used in the Go community for developing CLI applications and tools. Some essential Cobra commands include `cobra init`, `cobra add`, `cobra run`, and `cobra build`. Learning how to use Cobra can help you create robust and user-friendly CLI applications in Go.

You can install Cobra using go get:

```bash
go get -u github.com/spf13/cobra@latest
```

You can visit the official website for more information on using Cobra: [Cobra Documentation](https://cobra.dev/)

**SpeedTest-CLI**

SpeedTest-CLI is a command-line interface for testing internet bandwidth using the Speedtest.net service. It allows you to measure your download and upload speeds, ping times, and other network metrics from the terminal. SpeedTest-CLI provides a simple and efficient way to check your internet connection speed without the need for a web browser. Some essential SpeedTest-CLI commands include `speedtest`, `speedtest --simple`, `speedtest --list`, and `speedtest --server <server_id>`. Learning how to use SpeedTest-CLI can help you troubleshoot network issues, monitor internet performance, and optimize your internet connection.

You can install SpeedTest-CLI using homebrew:

```bash
brew install speedtest-cli
```

or, you can follow the installation instructions on the official GitHub repository: [SpeedTest-CLI Installation Guide](https://github.com/sivel/speedtest-cli)

These tools can help you enhance your development workflow, automate repetitive tasks, and streamline your command-line experience. By mastering these CLI tools, you can become more productive, efficient, and effective in your development work. Happy coding! 🚀
