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
   tetris block. This class is inherited from :py:class:`Action`.

   :param str direction: The direction of an active tetris block.
   :param repeat: How many times one should do the movement.

   .. py:method:: applyAction(board)

      Applying the movement with the direction as defined at :py:attr:`direction`.

.. py:class:: SetBlock(block)

   An :py:class:`Action` class which sets the active block on a board

.. py:class:: Block(rotation)

   A class which describes a block an its rotation. Internally,
   :py:attr:`rotations` contains a list of all
   rotations. :py:attr:`rotation_index` 

   :param int rotation_index: This contains the index which the
			      methods in this class use to determine
			      its rotation state.
   :param rotations: A list of the all possible rotations of the blocks.
		     
   .. py:method:: rotate

      Rotate the block counterclockwise; that is, increment
      :py:attr:`rotation_index` with 1.

   .. py:method:: getNextRotation

      Get the next rotation of the block.

      :return: The next rotation of the block.
      :rtype: list(list(int)).

   .. py:method:: getNextSize

      :return: The size of the next rotation as (x, y).
      :rtype: tuple(int, int)

   .. py:method:: getSize

      :return: The size of the current rotation as (x, y).
      :rtype: tuple(int, int)

   .. py:method:: getBlock

      :return: The block as a nested int array.
      :rtype: list(list(int))

.. py:class:: Board

   This class contains the tetris board.

   :param active_block: The current active block
   :type active_block: Block

   :param active_block_position: The position of the active block.
   :type active_block_position: tuple(int, int)
		       
   :param blocks: All the possible blocks for a board.
   :type blocks: dict(str, Block)
		 
   :param board: The board, where the value of a block at (x,y) is
                 defined as board[y][x].
   :type board: int

   .. py:method:: initialiseBlocks

      An internal function which creates all the blocks for the Tetris board.

   .. py:method:: getAvailableBlocks

      :return: Returns all availble blocks.
      :rtype: list(str)

   .. py:method:: getNewXYCoordinateWithDirection(direction)

      Takes a direction string and returns a new coordinate based on
      the current active block position at
      :py:attr:`active_block_position`.

      :param str direction: The direction
      :return: The new coordinate as (x, y).
      :rtype: tuple(int, int)
   
   .. py:method:: getNumberOfNonZeroesForEachRow

      Counts the number of non zeroes for each row.

      :return: Number of non zeroes for each row.
      :rtype: list(int)

   .. py:method:: setActiveBlockFromString(block_str)

      Sets the active block given a string.

      :param str block_str: The block shape as a string.

   .. py:method:: setActiveBlock(block)

      Sets the active block given a :py:class:`Block`.

      :param Block block: The block shape.

   .. py:method:: rotateActive

      Rotates the active block at :py:attr:`active_block`, does
      internally a collision check using
      :py:meth:`collisionCheckWithShapeAndPos`.

   .. py:method:: traverse(direction)

      Will traverse the active block using the direction and the
      method :py:meth:`getNewXYCoordinateWithDirection` if the
      collision check passes using :py:meth:`collisionCheck`.

      :param str direction: The direction of the block. Valid values
                            are: left, down and right.

   .. py:method:: addShape(position, block)

      Adds a block shape onto the board at a given position.

      :param tuple(int, int) position: The position which the shape are drawn onto.
      :param Block block: The block which is going to be drawn.
      :return: A board including the new shape.
      :rtype: list(list(int))

   .. py:method:: applyAction(action)

      Applies an :py:class:`Action` to the board; that is, the method
      :py:meth:`Action.applyAction` is called with the
      :py:class:`Board` as its argument.

   .. py:method:: collisionCheck(direction)

      Does a collision check for a given direction.

      :param str direction: A direction. Valid values are 'left',
                            'down' and 'right'.
      :return: Returns True if there is a collision, otherwise False.
      :rtype: Bool

   .. py:method:: collisionCheckWithShapeAndPos(position, block):

      Apply a given block onto the board with a given coordinate,
      then, check whether there is a collision or not.

      :param position: The position of the block in (x, y)
      :type position: tuple(int, int)
      :param Block block: The block
      :return: ``True`` if there is a collision, ``False`` otherwise.
      :rtype: Bool

   
   .. py:method:: doHardDrop

      Makes the active block go directly to the bottom of the board.


   .. py:method:: fillNullRowsFromTop(board, n)

      Adding null blocks from the top of the board and sets the result
      to :py:attr:`board`.

      :param board: The board.
      :param n: How many null rows one should add.


   .. py:method:: mergeActiveWithBoard

      Merges the active block with the board.

      :return: The resulting board.
      :rtype: list(list(int))

   .. py:method:: printBoard(board)

      Prints the board to the terminal.

      :param board: The board.
      :type board: list(list(int))

   .. py:method:: removeRows(row)

      Takes an array of integers and remove it from the board.

      :param row: Array of integers to remove.
      :type row: list(int)

   .. py:method:: update

      This method's purpose is to determine whether the active block
      should merge to the static one. Runs for each tick.

      
		  
