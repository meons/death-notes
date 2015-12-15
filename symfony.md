#Symfony

### Controller actions
* indexAction(): show entities
* showAction(): show entity
* newAction(): create entity
* editAction(): edit entity
* deleteAction(): delete entity

### deleteAction() example
```php
/**
     * Deletes a Category entity.
     *
     * @Route("/{id}", name="category_delete")
     * @Method("DELETE")
     */
    public function deleteAction(Request $request, Category $category)
    {
        $quiz = $category->getQuiz();
        $form = $this->createDeleteForm($category);
        $form->handleRequest($request);

        if ($form->isSubmitted() && $form->isValid()) {
            $em = $this->getDoctrine()->getManager();
            $em->remove($category);
            $em->flush();
        }

        $this->addFlash('success', 'changes_saved');

        return $this->redirectToRoute('quiz_edit', array(
            'id' => $quiz->getId(),
            'tab_enabled' => 'tab-category',
        ));
    }

    /**
     * Creates a form to delete a Category entity.
     *
     * @param Category $category The Category entity
     *
     * @return \Symfony\Component\Form\Form The form
     */
    private function createDeleteForm(Category $category)
    {
        return $this->createFormBuilder()
            ->setAction($this->generateUrl('category_delete', array('id' => $category->getId())))
            ->setMethod('DELETE')
            ->getForm()
        ;
    }
```

### Create form class example
```php
class CategoryType extends AbstractType
{
  /**
   * @param FormBuilderInterface $builder
   * @param array $options
   */
  public function buildForm(FormBuilderInterface $builder, array $options)
  {
    $builder->add('name');
  }
  
  /**
   * @param OptionsResolver $resolver
   */
  public function configureOptions(OptionsResolver $resolver)
  {
    $resolver->setDefaults(array(
      'data_class' => 'AppBundle\Entity\Category'
    ));
  }
  
  /**
   * @return string
   */
  public function getName()
  {
    return 'app_category';
  }
}
```
