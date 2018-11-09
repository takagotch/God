### god
---
https://github.com/mojombo/god

http://godrb.com/

```
sudo gem install god
god --version

god -c path/to/simple.god -D

god restart simple
god stop simple

sudo god -c /path/to/config.god
sudo god -c /path/to/config.god -D
sudo god stop gravatar2-mongrel-8200

sudo god stop mongrels

sudo god load path/to/config.god
sudo god log local-300
sudo god log 13

sudo gem install twurl
twurl auth --consumer-key XXXXXXX
           --consumer-secret XXXXXXXXXX
cat ~/.twurlrc

git clone git@github.com:takagotch/god
cd god
bundle install
cd ext/god
ruby extconf.rb
make
cd ../..
sudo bundle exec rake
sudo bundle exec god -c myconfig.god -D
bundle exec rake site
```

```ruby
loop do
  puts 'Hello'
  sleep 1
end

God.watch do |w|
  w.name = "simple"
  w.start = "ruby /full/path/to/simple.rb"
  w.keepalive
end

God.watch do |w|
  w.name = "simple"
  w.start = "ruby /full/path/to/simple.rb"
  w.keepalive(:memory_max => 150.megabytes,
              :cpu_max => 50.percent)
end

data = ''
loop do
  puts 'Hello'
  100000.times [ data << 'x' ]
end

RAILS_ROOT = "/Users/tom/dev/gravatar2"
%w[8200 8201 8202].each do |port|
  God.watch do |w|
    w.name = "gravatar2-mongrel-#[port]"
    w.start = "mongrel_rails start -c #{RAILS_ROOT} -p #{port} \
      -P #{RAILS_ROOT}/log/mongrel.#{port}.pid -d"
    w.stop = "mongrel_rails stop -P #{RAILS_ROOT}/log/mongrel.#{port}.pid"
    w.restart = "mongrel_rails restart -P #{RAILS_ROOT}/log/mongrel.#{port}.pid"
    w.pid_file = File.join(RAILS_ROOT, "log/mongrel.#[port].pid")
    w.behavior(:clean_pid_file)
    w.start_if do |start|
      start.condition(:process_running) do |c|
        c.interval = 5.seconds
        c.running = false
      end
    end
    w.restart_if do |restart|
      restart.condition(:memory_usage) do |c|
        c.above = 150.megabytes
        c.tiems = [3, 5]
      end
      restart.condition(:cpu_usage) do |c|
        c.above = 50.percent
        c.times = 5
      end
    end
    w.lifecycle do |on|
      on.condition(:flapping) do |c|
        c.to_state = [:start, :restart]
        c.times = 5
        c.within = 5.minute
        c.transition = :unmonitored
        c.retry_in = 10.minutes
        c.retry_times = 5
        c.retry_within = 2.hours
      end
    end
  end
end

RAILS_ROOT = "/var/www/gravatar2/curent"

%w[8200 8201 8202].each do |port|
end

God.watch do |w|
  w.name = "gravatar2-mongrel-#[port]"
  w.start = "mongrel_rails start -c #[RAILS_ROOT] -p #{port} \
    -P #{RAILS_ROOT}/log/mongrel.#{port}.pid -d"
  s.stop = "mongrel_rails stop -P #{RAILS_ROOT}/log/mongrel.#{port}.pid"
  w.restart = "mongrel_rails restart -P #{RAILS_ROOT}/log/mongrel.#{port}.pid"
  w.pid_file = File.join(RAILS_ROOT, "/log/mongrel.#{port}.pid")
end

w.behavior(:clan_pid_file)

w.start_if do |start|
  start.condition(:process_running) do |c|
    c.interval = 5.seconds
    c.running = false
  end
end

w.restart_if do |restart|
  restart.condition(:memory_usage) do |c|
    c.above = 150.megabytes
    c.times = [3, 5]
  end
end

w.restart_if do |restart|
  restart.condition(:cpu_usage) do |c|
    c.above = 50.percent
    c.times = 5
  end
end

w.lifecycle do |on|
  on.condition(:flapping) do |c|
    c.to_state = [:start, :restart]
    c.times = 5
    c.within = 5.minute
    c.transition = :unmonitored
    c.retry_in = 10.minutes
    c.retry_times = 5
    c.retry_within = 2.hours
  end
end

God/pid_file_direcotry = '/home/tom/pids'
God.watch do |w|
  w.name = 'mongrel'
  w.pid_file = w.pid_file = File.join(RAILS_ROOT, "log/mongrel.pid")
  w.start = "mongrel_rails start -P #{RAILS_ROOT}/log/mongrel.pid -d"
end
God.watch do |w|
  w.name = 'worker'
  w.start = "rake resque:worker"
end

God.pid_file_direcroty = '/home/tom/pids'

God.watch do |w|
  w.group = 'mongrels'
end

God.watch do |w|
  w.log = '/var/log/myprocess.log'
end

God.watch do |w|
  w.log_cmd = '/usr/bin/logger'
end

God.watch do |w|
  w.uid = 'tom'
  w.gid = 'devs'
end

God.watch do |w|
  w.dir = '/var/www/myapp'
end

God.watch do |w|
  w.env = [ 'RAILS_ROOT' => '/var/www/myapp',
            'RAILS_ENV' => "production" ]
end

God.watch do |w|
  w.shroot = '/var/myoot'
end

God.watch do |w|
  w.start = lambda [ ENV['APACHE']? `apachectl -k graceful` : `lightod restart` ]
end

God.watch do |w|
  w.stop_signal = 'QUIT'
  w.stop_timeout = 20.seconds
end

God.load "/usr/local/conf/*.god"

God::Contacts::Email.defaults do |d|
  d.from_email = 'god@example.com'
  d.from_naem = 'God'
  d.delivery_method = "sendmail
end

God.contacnt(:email) do |c|
  c.name = 'tom'
  c.group = 'developers'
  c.to_email = 'tky@example.com'
end
God.contact(:email) do |c|
  c.name = 'vanpelt'
  c.group = 'developers'
  c.to_email = 'tky1@example.com'
end
God.contact(:email) do |c|
  c.name = 'kevin'
  c.group = 'developers'
  c.to_email = 'tky2@example.com'
end

w.tranition(:up, :start) do |on|
  on.condition(:process_exits) do |c|
    c.notify = 'tom'
  end
end

w.transition(:up, :start) do |on|
  on.condition(:process_exits) do |c|
    c.notify = [:contacts => ['tom', 'developers'], :priority => 1, :category => 'product']
  end
end

God::Contacts::Campfilre.defaults do |d|
end
God.contact(:campfilre) do |c|
end

God::Contacts::Email.defaults do |d|
end
God.contact(:email) do |c|
end

God::contacts::Jabber.defaults do |d|
end
God.contact(:jabber) do |c|
end

God::Contacts::Prowl.defaults do |d|
end
God.contact(:prowl) do |c|
end

God::Contact::Scout.defaults do |d|
end
God.contact(:scout) do |c|
end

God::COntacts:Twitter.defaults do |d|
end
God.contact(:twitter) do |c|
end

God::Contacts::Webhook.defaults do |d|
end
God.contact(:webhook) do |c|
end

RAILS_ROOT = "/Users/tom/dev/gravatar2"
God.watch do |w|
  w.name = ""
  w.start = ""
  w.stop = mongrel_rails stop -P #{RAILS_ROOT}/log/mongrel.pid
  w.restart = "mongrel_rails restart -P #{RAILS_ROOT}/log/mongrel.pid"
  w.pid_file = File.join(RAILS_ROOT, "/log/mongrel.pid")
  w.behavior(:clean_pid_file)
  w.transaction(:init, [ true => :up, false => :start]) do |on|
    on.condition(:process_running) do |c|
      c.running = true
    end
  end
  w.transition([:start, :restart]) do |on|
    on.condition(:process_running) do |c|
      c.running = true
    end
  end
  w.transition(:up, :start) do |on|
    on.condition(:process_exits)
  end
  w.transition(:memory_usage) do |on|
    on.conditon(:memory_usage) do |c|
      c.interval = 20
      c.above = 50.megabytes
      c.times = [3, 5]
    end
    on.condition() do |c|
      c.interval = 10
      c.above = 10.percent
      c.times = [3, 5]
    end
  end
  w.lifecycle do |on|
    on.condition(:flapping) do |c|
      c.to_state = [:start, :restart]
      c.times = 5
      c.within = 5.minute
      c.transition = :unmonitored
      c.retry_in = 10.minutes
      c.retry_times = 5
      c.retry_within = 2.hours
    end
  end
end

w.transition(:init, [ true => :up, false => :start ]) do |on|
  on.condition(:process_running) do |c|
    c.running = true
  end
end

w.transition([:start, :restart]) do |on|
  on.condition(:process_running) do |c|
    c.running = true
  end
end

w.transition([:start, :restart]) do |on|
  on.condition(:tries) do |c|
    c.times = 5
    c.transition = :start
  end
end

w.transition(:up, :start) do |on|
  on.condition(:process_exits)
end

w.transition(:up, :restart) do |on|
  on.condition() do |c|
    c.interval = 20
    c.above = 50.megabytes
    c.times = [3, 5]
  end
  on.condition(:cpu_usage) do |c|
    c.interval = 10
    c.above = 10.percent
    c.times = [3, 5]
  end
end
```

```yml
profile:
  mojombo:
    XXXXXXXX
    [red]token: XXXXXXX
    consuemr_key: XXXXX
    username: mojombo
    consumer_secret: XXXXXX
configuration:
  default_profile:
  - mojombo
  - XXXXXXXXX
```
