Tetrislib
=========

.. py:class:: Action

   Every class which are a subset to this class is an action which
   operates on a board; that is, they guarantee that they have the
   method :py:meth:`applyAction`.

   :param bool action_completed: Indicates whether the action has been
                                 completed or not.
   
   .. py:method:: applyAction(board)

      Do stuff; then, set :py:attr:`action_completed` to True.

.. py:class:: Movement(direction, [repeat=1])

   Movement is a class which describes the direction of the active
   tetris block.

   :param str direction: The direction of an active tetris block.
   :param repeat: How many times one should do the movement.

   .. py:method:: applyAction(board)

      Applying the movement with the direction as defined at :py:attr:`direction`.

   
			     
