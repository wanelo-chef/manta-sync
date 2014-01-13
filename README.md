manta-sync
==========

This Chef cookbook installs manta-sync via NPM.

## Requirements

An `npm` cookbook. For instance, https://github.com/balbeko/chef-npm


## Usage

Add the `manta-sync::default` recipe to a run list or use `include_recipe` to
install manta-sync.

This cookbook does not configure manta-sync to run automatically, nor does it
do any key management. Use another cookbook, such as https://github.com/wanelo-chef/manta
in order to configure keys.

An application-specific recipe can use the cron provider to automatically set
up manta-sync to run:

```ruby
include_recipe 'manta::client' # install keys
include_recipe 'manta-sync'

cron 'Upload files into manta' do
  minute '30'
  hour '5'
  day '*'
  home '/root'
  command %Q{source /root/.manta_config && manta-sync -m /path/to/files/ ~~/stor/path/to/files}
end
```
