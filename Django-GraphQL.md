```
class ValidationMutation(graphene.Mutation):
    class Arguments:
        field1 = graphene.String()
        field2 = graphene.String()

    def validate_field1(self, value):
        if value != 'BAD':
            return value
        raise graphene.FieldError('field1 is BAD')

    def validate_field2(self, value):
        if value != 'OOPS':
            return value
        raise graphene.FieldError('field1 is OOPS')

    def validate(self, fields):
        field1 = fields.get('field1', None)
        field2 = fields.get('field2', None)
        if field1 == field2:
            raise graphene.FieldError('fields are the same value')
        return fields

    def mutate(self, field1, field2):
        # This should be done with a loop through arguments
        self.validate_field1(field1)
        self.validate_field2(field2)
        self.validate({
            'field1':field1, 
            'field2':field2
        })
        return ValidationMutation()
