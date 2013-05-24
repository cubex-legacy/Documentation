<a name="baseattribute"></a>
###Base Attribute

There are plenty of things you can do with an attribute, however, they are pretty
obvious, so you can find the [information here](http://api.cubex.io/class-Cubex.Data.Attribute.Attribute.html)

<a name="composite"></a>
###Composite Attributes

A composite attribute acts as a single container or group for multiple attributes
that exist within your mapper.  This allows you to assign an array to a single attribute
which will push the data out to the raw attributes on your mapper, for them to be
saved in your database as separate attributes.

  class Example extends DataMapper
  {
    public $address;

    protected function _configure()
    {
      $this->_addCompositeAttribute(
        "address",
        ["addressLine1", "addressLine2", "city", "postcode"]
      );
    }
  }

  $example = new Example();
  $example->address = ["Line 1","Line 2", "Portsmouth", "PO15 XXX"];
  $example->saveChanges();

  //Your database will contain 4 columns, matching the split out address

<a name="compound"></a>
###Compound Attributes

A compound attribute will store multiple attributes down to a single column within
your database.  This allows you to work with individual attributes on a mapper,
and be able to store the data within a single column.

  class Example extends DataMapper
  {
    public $addressLine1;
    public $addressLine2;
    public $city;
    public $postcode;

    protected function _configure()
    {
      $this->_addCompoundAttribute(
        "address",
        ["addressLine1", "addressLine2", "city", "postcode"]
      );
    }
  }

  $example = new Example();
  $example->city = "Portsmouth";
  $example->saveChanges();

  //Your database for this mapper will contain a single "address" column


<a name="polymorphic"></a>
###Polymorphic Attributes

A Polymorphic attribute acts as a container for other mappers, within a single
attribute on your mapper.  If you wish to link a generic mapper onto another mapper
you can set and get from your attribute as if it were a standard data mapper,
with the added benefit of the data being stored in the database simply being the
class (type) of the external mapper and the id.  This will result in two columns
being created in your data source, based on the attribute name.  e.g.

  class Example extends DataMapper
  {
    public $child;
    public $name;

    protected function _configure()
    {
      $this->_addPolymorphicAttribute("child");
    }
  }

  $example = new Example(1);
  $example->name = "Parent";
  $example->child = new Example(2);
  $example->child->name = "Child";
  $example->child->saveChanges();
  $example->saveChanges();

  $loader = new Example(1);
  echo $loader->child->name; //Child

<a name="callback"></a>
###Callback Attributes

A Callback attribute allows you to call a method when your attribute is being
saved.  You also have the ability to disable saving of this attribute to the
original data source, which gives you the flexibility to contain an attribute
within one mapper, but save the data to a different location, which could be
through another mapper, or even by doing an API call to save that specific value.

To add a callback attribute, you just need to construct the attribute and add
it to your mapper.

  class Example extends DataMapper
  {
    public $caller;

    protected function _configure()
    {
      $attr = new CallbackAttribute("caller");
      $attr->setCallback([$this, "saveProperty"]);
      $attr->setStoreOriginal(false);
      $this->_addAttribute($attr);
    }

    public function saveProperty(CallbackAttribute $attr)
    {
        $attr->data(); //Current value of the attribute
        $attr->name(); //Name of the attribute
    }
  }
