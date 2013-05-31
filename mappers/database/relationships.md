RecordMapper Relationships
==

Returning a relationship from your mapper through a method, allows you to easily access related mappers/objects,
and will also allow you to prefetch the results of these mappers with optimised database queries.

These relationships make working with mappers a lot easier, and can optimise your database access.

###hasOne


  public function child()
  {
    return $this->hasOne(new Mapper);
  }

###hasMany

  public function children()
  {
    return $this->hasMany(new Mapper);
  }

###belongsTo

  public function parent()
  {
    return $this->belongsTo(new Mapper);
  }

###hasAndBelongsToMany



  public function relative()
  {
    return $this->hasAndBelongsToMany(new Mapper);
  }