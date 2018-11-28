# Mac Development Ansible Playbook

[![Build Status](https://travis-ci.org/afirth/mac-dev-playbook.svg?branch=master)](https://travis-ci.org/afirth/mac-dev-playbook)

This playbook installs and configures most of the software I use on my Mac for web and software development. Some things in macOS are slightly difficult to automate, so I still have some manual installation steps, but at least it's all documented here.

This is a work in progress, and is mostly a means for me to document my current Mac's setup. I'll be evolving this set of playbooks over time.

## Installation

  1. Ensure Apple's command line tools are installed (`xcode-select --install` to launch the installer).
      - `xcode-select --install`
  2. [Install Ansible](http://docs.ansible.com/intro_installation.html).
      - `sudo easy_install pip`
      - `sudo pip install ansible`
  3. Clone this repository to your local drive.
      - `mkdir ~/git && cd ~/git/ && git clone https://github.com/afirth/mac-dev-playbook`
  4. Install required Ansible roles.
      - `cd ~/git/mac-dev-playbook && ansible-galaxy install -r requirements.yml`
  5. Run the main playbook. Enter your account password when prompted.
      - `cd ~/git/mac-dev-playbook && ansible-playbook main.yml -i inventory -K`

> Note: If some Homebrew commands fail, you might need to agree to Xcode's license or fix some other Brew issue. Run `brew doctor` to see if this is the case.

### Running a specific set of tagged tasks

You can filter which part of the provisioning process to run by specifying a set of tags using `ansible-playbook`'s `--tags` flag. The tags available are `dotfiles`, `homebrew`, `mas`, `extra-packages` and `osx`.

    ansible-playbook main.yml -i inventory -K --tags "dotfiles,homebrew"

## Overriding Defaults

Not everyone's development environment and preferred software configuration is the same.

You can override any of the defaults configured in `default.config.yml` by creating a `config.yml` file and setting the overrides in that file.
Any variable can be overridden in `config.yml`; see the supporting roles' documentation for a complete list of available variables.

## Included Applications / Configuration (Default)

My [dotfiles](https://github.com/afirth/dotfiles) are also installed into the current user's home directory, including the `.osx` dotfile for configuring many aspects of macOS for better performance and ease of use. You can disable dotfiles management by setting `configure_dotfiles: no` in your configuration.

Finally, there are a few other preferences and settings added on for various apps and services.

## Future additions

### Things that still need to be done manually

It's my hope that I can get the rest of these things wrapped up into Ansible playbooks soon, but for now, these steps need to be completed manually (assuming you already have Xcode and Ansible installed, and have run this playbook).

  1. Configure 3 finger click for middle click in BTT. Add license for BTT.
  1. Set JJG-Term as the default Terminal theme (it's installed, but not set as default automatically).
  2. Install [Sublime Package Manager](http://sublime.wbond.net/installation).
  3. Install all the apps that aren't yet in this setup (see below).
  4. Remap Caps Lock to Escape (requires macOS Sierra 10.12.1+).
  5. Set trackpad tracking rate.
  6. Set mouse tracking rate.
  7. Configure extra Mail and/or Calendar accounts (e.g. Google, Exchange, etc.).
      - open chrome and navigate to www.gmail.com - click icon right side of address bar

### Applications/packages to be added:

These are mostly direct download links, some are more difficult to install because of custom installers or other nonstandard install quirks:

  - [iShowU HD](http://www.shinywhitebox.com/downloads/iShowU_HD_2.3.20.dmg)
  - [Adobe Creative Cloud](http://www.adobe.com/creativecloud.html)

### Vim Configuration

  - Vim Plug is autoloaded by the vimrc the first time you open vim

## Testing the Playbook

Many people have asked me if I often wipe my entire workstation and start from scratch just to test changes to the playbook. Nope! Instead, I posted instructions for how I build a [Mac OS X VirtualBox VM](https://github.com/geerlingguy/mac-osx-virtualbox-vm), on which I can continually run and re-run this playbook to test changes and make sure things work correctly.

Additionally, this project is [continuously tested on Travis CI's macOS infrastructure](https://travis-ci.org/afirth/mac-dev-playbook).

## Ansible for DevOps

Check out [Ansible for DevOps](https://www.ansiblefordevops.com/), which teaches you how to automate almost anything with Ansible.

## Author

[@afirth](github.com/afirth) 2018, forked from[Jeff Geerling](https://www.jeffgeerling.com/), 2014 (originally inspired by [MWGriffin/ansible-playbooks](https://github.com/MWGriffin/ansible-playbooks)).
