from django.db import models
from django.contrib.auth import get_user_model
User = get_user_model()
class Mystery(models.Model):
    """A simple mystery model."""
    title = models.CharField(max_length=32)
    description = models.TextField()
    reported_date = models.DateTimeField(auto_now=True)
    reported_by = models.ForeignKey(User,related_name="reported_mysteries",on_delete=models.CASCADE)
    is_verified = models.BooleanField(default=False)
    def __str__(self):
        return "{}-{}".format(self.title, self.is_verified)
class MysteryResolution(models.Model):
    mystery = models.OneToOneField(Mystery, related_name='resolution', on_delete=models.CASCADE)
    resolved_by = models.ForeignKey(User, related_name='resolutions', on_delete=models.CASCADE)
    notes = models.TextField(null=True, blank=True)
