*   Extracted `ActiveRecord::AttributeAssignment` to `ActiveModel::AttributeAssignment`
    allowing to use it for any object as an includable module

    ``` ruby
    class Cat
      include ActiveModel::AttributeAssignment
      attr_accessor :name, :status
    end

    cat = Cat.new
    cat.assign_attributes(name: "Gorby", status: "yawning")
    cat.name # => 'Gorby'
    cat.status => 'yawning'
    cat.assign_attributes(status: "sleeping")
    cat.name # => 'Gorby'
    cat.status => 'sleeping'
    ```

    *Bogdan Gusiev*

*   Add `ActiveModel::Errors#details`

    To be able to return type of used validator, one can now call `details`
    on Errors instance:

    ```ruby
    class User < ActiveRecord::Base
      validates :name, presence: true
    end
    ```

    ```ruby
    user = User.new; user.valid?; user.errors.details
    => {name: [{error: :blank}]}
    ```

    *Wojciech Wnętrzak*

*   Change validates_acceptance_of to accept true by default.

    The default for validates_acceptance_of is now "1" and true.
    In the past, only "1" was the default and you were required to add
    accept: true.

*   Remove deprecated `ActiveModel::Dirty#reset_#{attribute}` and
    `ActiveModel::Dirty#reset_changes`.

    *Rafael Mendonça França*

*   Change the way in which callback chains can be halted.

    The preferred method to halt a callback chain from now on is to explicitly
    `throw(:abort)`.
    In the past, returning `false` in an ActiveModel or ActiveModel::Validations
    `before_` callback had the side effect of halting the callback chain.
    This is not recommended anymore and, depending on the value of the
    `config.active_support.halt_callback_chains_on_return_false` option, will
    either not work at all or display a deprecation warning.


Please check [4-2-stable](https://github.com/rails/rails/blob/4-2-stable/activemodel/CHANGELOG.md) for previous changes.
