# JavaScript-Binary-tree-lock
Problem asked by Google

```
class LockingTreeNode {
  /**
   * Initialize a binary tree node with a value and/or left and right nodes
   
   */
  constructor(val, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;

    this.isLocked = false;
    this.parent = null;
    this.lockedDescendantCount = 0;
  }
}

/**
 * Checks to see if we can lock or unlock this node by checking ancestors and descendants
 */
function canLockOrUnlock(node) {
  if (node.lockedDescendantCount > 0) return false;

  let curr = node.parent;
  while (curr !== null) {
    if (curr.isLocked) return false;
    curr = curr.parent;
  }
  return true;
}

/**
 * Return whether the node is locked
 */
function isLocked(node) {
  return node.isLocked;
}

/**
 * Tries to lock the node. If it cannot be locked, then it should return false.
 * Otherwise, it should lock it and return true.
 */
function lock(node) {
  if (node === null) return false;
  if (!node.isLocked && canLockOrUnlock(node)) {
    // Not locked, so update isLocked and increment count in all ancestors
    node.isLocked = true;

    let curr = node.parent;
    while (curr !== null) {
      curr.lockedDescendantCount += 1;
      curr = curr.parent;
    }
    return true;
  }
  return false;
}

/**
 * Unlocks the node.
 * If it cannot be unlocked, then it should return false.
 * Otherwise, it should unlock it and return true
 */
function unlock(node) {
  if (node === null) return false;

  if (node.isLocked && canLockOrUnlock(node)) {
    node.isLocked = false;

    // Update count in all ancestors
    let curr = node.parent;
    while (curr !== null) {
      curr.lockedDescendantCount -= 1;
      curr = curr.parent;
    }
    return true;
  }
  return false;
}
export { LockingTreeNode, isLocked, lock, unlock };
```
