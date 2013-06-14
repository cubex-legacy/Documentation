##Configuration

###Introduction
All configurations for a Cubex project are stored within the conf directory.
Cubex configurations are stored with ini files (based on some speed testing)
and will include defaults.ini and {CUBEX_ENV}.ini by default.

The method by which configs are included and which configs are included can be
changed within public/index.php and bin/cubex.
Cubex just takes an array of configs which must be stored within groups.

  $config = ['project' => [], 'response' => []];
  $config['project'] = ['source' => 'src', 'namespace' => 'Project'];
  $config['response'] = ['minify_html' => true];
