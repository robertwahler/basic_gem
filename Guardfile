require 'rbconfig'
WINDOWS = RbConfig::CONFIG['host_os'] =~ /msdos|mswin|win32|mingw/i unless defined?(WINDOWS)

notification :on

# @examples
#
#     guard --group specs
#     guard --group features
#
group :rspec do
  guard 'rspec',
        :all_after_pass => false,
        :all_on_start => false,
        #:cli => '--color --format nested --fail-fast',
        :cli => '--color --format nested',
        :version => 2 do

    watch(%r{^spec/.+_spec\.rb$})
    watch('spec/spec_helper.rb')                              { "spec" }

    # root folder
    watch(%r{^lib/basic_gem.rb$})                             { "spec/basic_gem" }

    # ex: lib/app_name/views.rb -> spec/app_name/views_spec.rb
    watch(%r{^lib/(.+)/(.+)\.rb$})                            { |m| "spec/#{m[1]}/#{m[2]}_spec.rb" }

    # ex: lib/app_name/views/view_helper.rb -> spec/app_name/views/view_helper_spec.rb
    watch(%r{^lib/(.+)/(.+)/(.+)\.rb$})                       { |m| "spec/#{m[1]}/#{m[2]}/#{m[3]}_spec.rb" }
  end
end

group :cucumber do

  opts =  []
  opts << ["--color"]
  opts << ["--format pretty"]
  opts << ["--strict"]
  opts << ["-r features"]
  opts << ["--no-profile"]
  #opts << ["--tags @focus"]
  opts << ["--tags ~@wip"]
  opts << ["--tags ~@manual"]
  opts << ["--tags ~@windows"] unless WINDOWS
  opts << ["--tags ~@posix"] if WINDOWS

  guard 'cucumber',
        :cli => opts.join(" "),
        :all_after_pass => false,
        :all_on_start => false do

    watch(%r{^features/.+\.feature$})
  end
end
