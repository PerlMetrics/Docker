Docker
======

Docker stuff used by Perl Metrics

## Docker image content

  * curl
  * [git](http://git-scm.com)
  
  * [PerlBrew](http://perlbrew.pl)
    * Perl 5.8.x
    * Perl 5.10.x
    * Perl 5.12.x
    * Perl 5.14.x
    * Perl 5.16.x
    * Perl 5.18.x

  * [cpanminus](https://metacpan.org/pod/App::cpanminus)
  
  * Perl Modules
    * [Dancer](perldancer.org)
    * [Dist::Zilla](https://metacpan.org/pod/Dist::Zilla)
    * [File::Slurp](https://metacpan.org/pod/File::Slurp)
    * [JSON](https://metacpan.org/pod/JSON)
    * [Moose](https://metacpan.org/pod/Moose)


## Docker run

We start by a system update/upgrade:
```
apt-get update
apt-get upgrade
```

Then, we update Perl modules for each Perl versions in PerlBrew:
```
perlbrew use perl-5.x
cpan-outdated -p | cpanm
perlbrew list-modules | perlbrew exec --with perl-5.x cpanm
...
perlbrew list-modules | perlbrew exec --with perl-5.x cpanm

```

Then, we get the GitHub repository which sends the hook:
```
git clone --depth=50 --branch=master git://github.com/<user>/<repo>.git <user>/<repo>

cd <user>/<repo>

git checkout -qf <id>
```

### Test suite

For each Perl versions in PerlBrew, we launch test suite:
```
dzil authordeps | xargs cpanm
dzil listdeps | xargs cpanm
dzil test
```

### Critic

### Coverage

### Kwalitee
